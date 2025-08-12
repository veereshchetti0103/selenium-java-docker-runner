pipeline {

    agent any

    parameters {
         choice choices: ['chrome', 'firefox'], description: 'Select the browser', name: 'Browser'
   }

    stages {
        stage('Start Grid') {
            steps {
                echo 'Starting Selenium Grid...'
                bat 'docker-compose -f grid.yaml up --scale %Browser%=2 -d'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'                
                bat 'docker-compose -f test-suites.yaml up'
                script{
                    if(fileExists('output/flight-reservation/testng-failed-report.html') || fileExists('output/vendor-portal/testng-failed-report.html')) {
                        echo 'Flight Reservation or Vendor Portal tests failed.'
                        error 'Tests failed.'
                    }
                }
            }
        }
              
    }
    post {
        always {
            echo 'Cleaning up...'
            bat 'docker-compose -f grid.yaml down'
            bat 'docker-compose -f test-suites.yaml down'
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', allowEmptyArchive: true ,followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', allowEmptyArchive: true, followSymlinks: false
        }
    }
}