pipeline {

    agent any

    stages {
        stage('Start Grid') {
            steps {
                echo 'Starting Selenium Grid...'
                bat 'docker-compose -f grid.yaml up -d'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'                
                bat 'docker-compose -f testsuites.yaml up'
            }
        }
              
    }
    post {
        always {
            echo 'Cleaning up...'
            bat 'docker-compose -f grid.yaml down'
            bat 'docker-compose -f test-suites.yaml down'
        }
    }
}