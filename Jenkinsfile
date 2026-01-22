pipeline {

  agent any

  environment {
    IMAGE_NAME = "devad14/jenkins-learning-pipeline"
    IMAGE_TAG  = "v.${BUILD_NUMBER}"
  }

	 stage("Buiding Docker Image") {
	   steps {
		 sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
		 
	   }
	 }
     
     stage("Pushing Docker Image to DockerHub") {
	   steps {
	         withCredentials([usernamePassword(credentialsId: 'docker-hub-login', passwordVariable: 'docker_pass', usernameVariable: 'docker_user')]) {
                 sh 'docker login -u $docker_user -p $docker_pass'
				 sh 'docker push ${IMAGE_NAME}:${IMAGE_TAG}'
				 
              }
	   }
	 }
		
	 }	 
  
