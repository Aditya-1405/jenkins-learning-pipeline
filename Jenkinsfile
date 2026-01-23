pipeline {

  agent any

  environment {
    IMAGE_NAME = "devad14/jenkins-learning-pipeline"
    IMAGE_TAG  = "v1.1.${BUILD_NUMBER}"
  }

  stages {

    stage("Branch Info") {
      steps {
        echo "Running on branch: ${env.BRANCH_NAME}"
      }
    }

    stage("Docker Build & Push") {
      when {
        branch 'main'
      }
      steps {
        sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."

        withCredentials([usernamePassword(
          credentialsId: 'docker-hub-login',
          usernameVariable: 'docker_user',
          passwordVariable: 'docker_pass'
        )]) {
          sh "docker login -u $docker_user -p $docker_pass"
          sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
        }
      }
    }

    stage("Multi Branch Demo Stages") {
      when {
        branch 'multi-branch-pipeline'
      }
      stages {
        stage("Stage 1") {
          steps {
            echo "This is stage 1!!!"
          }
        }

        stage("Multi Branch Pipeline Setup") {
          steps {
            echo "Congrats on setting a multi-branch pipeline successfully !!!"
          }
        }
      }
    }
  }
}

