pipeline {
    agent any

    parameters {
      choice choices: ['Chrome', 'Firefox'], description: 'Select a browser', name: 'BROWSER'
    }

    stages {
        stage('Start Grid') {
            steps {
                sh "docker-compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"
            }
        }
        stage('Run Test suite') {
            steps {
                sh 'docker-compose -f test-suite.yaml up'
            }
        }
    }
    post {
        always {
            sh 'docker-compose -f grid.yaml down'
            sh 'docker-compose -f test-suite.yaml down'
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', followSymlinks: false
        }
    }
}
