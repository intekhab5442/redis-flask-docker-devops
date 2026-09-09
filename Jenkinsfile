pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                Checkout scm
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
