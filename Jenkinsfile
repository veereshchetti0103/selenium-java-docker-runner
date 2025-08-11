pipeline {
    agent any

    stages {
        stage('Run Test') {
            steps {
                echo 'Docker compose up...'
                sh 'docker-compose up -d'
            }
        }
        stage('Bring Down') {
            steps {
                echo 'Docker compose down...'
                sh 'docker-compose down'
            }
        }
        
    }
}