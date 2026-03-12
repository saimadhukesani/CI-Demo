pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t myapp .'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker stop myapp-container || exit 0'
                bat 'docker rm myapp-container || exit 0'
                bat 'docker run -d -p 8081:8080 --name myapp-container myapp'
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}
