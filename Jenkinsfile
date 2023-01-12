pipeline{

	agent {label 'VPS'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('DockerHub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git branch: 'main', url:'https://github.com/Dagaral02/SRI_Dagaral02'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t dagaral02/jenkins:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push dagaral02/jenkins:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
