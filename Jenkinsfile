pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building The project' 
                bat './mvnw clean' 
            }
        }
        stage('Test'){
            steps {
                echo 'Running the test in the project'
                bat './mvnw test'
            }
        }
        stage('package'){
            steps{
                echo 'Packaging stage has been executed'
                bat './mvnw package'
            }
              
        }
        stage('Deploy') {
              steps {
                  echo 'Deploying stage has been executed'
                  bat './mvnw deploy'
              }
        }
    }
}
