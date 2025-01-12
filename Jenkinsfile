pipeline {
    agent any
    stages {
        stage('Start Grid') {
            steps {
                sh 'docker-compose -f grid.yaml up -d'
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
        }
    }
}
