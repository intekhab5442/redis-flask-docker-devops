pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                checkout scm
            }
        }
        stage ('build') {
            steps {
                sh 'docker compose build'
            }
        }
        stage ('Deploy') {
            steps {
                sh 'docker compose up -d'
            }
        }
        stage ('verify') {
            steps {
                sh 'docker compose ps'
                sh 'curl -f http://localhost:5001/'
            }
        }
    }

    post {
        always {
            sh 'docker compose ps'
        }
    }
}
