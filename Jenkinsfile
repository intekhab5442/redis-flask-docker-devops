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
	stage ('test') {
            steps {
                sh 'docker compose run --rm flask pytest'
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
		sh '''
                    for i in {1..10}; 
                    do
                        curl -f http://localhost:5001/ && exit 0
                        sleep 2
                    done
                    exit 1

                '''
               
            }
        }
    }

    post {
        always {
            sh 'docker compose ps'
        }
	cleanup{
            sh 'docker image prune -f || true'
        }
    }
}
