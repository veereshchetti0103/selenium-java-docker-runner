pipeline {
    agent any

    stages {
        stage('Run Test') {
            steps {
                echo 'Docker compose up...'
                bat 'docker-compose up -d'
            }
        }
        stage('Bring Down') {
            steps {
                echo 'Docker compose down...'
                bat 'docker-compose down'
            }
        }
        
    }
}