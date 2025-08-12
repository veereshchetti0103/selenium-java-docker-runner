pipeline {

    agent any

    stages {
        stage('Start Grid') {
            steps {
                echo 'Starting Selenium Grid...'
                sh 'docker-compose -f grid.yaml up -d'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'                
                sh 'docker-compose -f testsuites.yaml up'
            }
        }
              
    }
    post {
        always {
            echo 'Cleaning up...'
            sh 'docker-compose -f grid.yaml down'
            sh 'docker-compose -f testsuites.yaml down'
        }
    }
}