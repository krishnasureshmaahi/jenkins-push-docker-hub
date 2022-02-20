pipeline{

	agent {label 'linux'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/shaik-byte/jenkins-push-docker-hub.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t shaikbyte/nodeapp_test:1.0 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push shaikbyte/nodeapp_test:1.0'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
