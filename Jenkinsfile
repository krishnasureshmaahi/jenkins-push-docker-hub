pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('Checkout') {
	        
	               steps {
                                git credentialsId: 'github', url: 'https://github.com/krishnasureshmaahi/jenkins-push-docker-hub.git'
                       }
	    }
	    
		stage('gitclone') {

			steps {
				git 'https://github.com/krishnasureshmaahi/jenkins-push-docker-hub.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t suresh1904/argo_cd:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push suresh1904/argo_cd:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
