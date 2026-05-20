pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                bat 'py -m pip install -r requirements.txt'
            }
        }

        stage('Dependency Check') {
            steps {
                bat 'py -m pip list'
            }
        }

        stage('Security Scan') {
            steps {
                bat 'py -m pip install safety'
                bat 'py -m safety check'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t smartpark .'
            }
        }

    }
}