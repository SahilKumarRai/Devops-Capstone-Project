pipeline {
    agent any
    environment {
	DOCKER_HUB_CREDS = credentials("capstone_docker")
    }
    stages {
	stage('Login to dockerhub') {
	   steps {
		script {
		    sh "docker login -u ${DOCKER_HUB_CREDS_USR} -p ${DOCKER_HUB_CREDS_PSW}"
		}
	}	
     }
	stage('Remove existing container if any') {
            steps {
                script {
		    try {
			sh "docker rm -f 202051167capstone_container"
		   } catch (e) {
			sh 'echo "Container does not exist"'	
		}
                }
        }       
      }
        stage('Building Website') {
            steps {
                sh 'docker build . -t 202051167capstone_image'
            }
       }

       stage('Testing Website') {
            steps {
                sh 'echo "Testing Website"'
            }
       }

       stage('Push to Production') {
            steps {
                sh 'docker run -it -p 82:80 -d --name 202051167capstone_container 202051167capstone_image'
            }
       }
    }
}