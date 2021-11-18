pipeline {
    agent {label 'slave-debian'}

    environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub_id')
		DOCKER_TAG = getVersion()
	}

    stages {

        stage('SCM'){
            steps{
 				// Get some code from a GitHub repository
                git branch: 'ansible', url: 'https://github.com/ayeliferov/spring.git'
            }
        }

		stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }

		stage('Docker Build'){
            steps{
                sh "docker build . -t ayeliferov/epam_lab:FinalProject_${DOCKER_TAG} "
            }
        }

			stage('DockerHub Push'){
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
				sh "docker push ayeliferov/epam_lab:FinalProject_${DOCKER_TAG} "
				sh 'docker logout'
			}
		}
	}
}



def getVersion(){
    def commitHash = sh label: '', returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}