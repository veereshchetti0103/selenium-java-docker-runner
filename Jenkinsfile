pipeline {

    agent any

    parameters {
         choice choices: ['chrome', 'firefox'], description: 'Select the browser', name: 'Browser'
   }

    stages {
        stage('Start Grid') {
            steps {
                echo 'Starting Selenium Grid...'
                sh 'docker-compose -f grid.yaml up --scale ${params.Browser}=2 -d'
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
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', allowEmptyArchive: true ,followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', allowEmptyArchive: true, followSymlinks: false
        }
    }
}