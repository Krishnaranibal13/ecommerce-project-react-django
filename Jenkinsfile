pipeline {
    agent any

    stages {

        stage('Check Files') {
            steps {
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Stop Old Containers') {
            steps {
                sh 'docker-compose down || true'
            }
        }

        stage('Build & Deploy') {
            steps {
                sh 'docker-compose up -d --build'
            }
        }

        stage('Run Migrations') {
            steps {
                sh 'docker exec django_backend python manage.py migrate'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Successful!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
