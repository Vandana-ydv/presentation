pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/Vandana-ydv/presentation.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Dependency Check') {
            steps {
                bat 'pip list'
            }
        }

        stage('Security Scan') {
            steps {
                bat 'pip install safety'
                bat 'safety check'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t smartpark .'
            }
        }

    }
}