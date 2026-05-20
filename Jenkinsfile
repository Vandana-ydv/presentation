pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                bat '"C:\\WINDOWS\\py.exe" -m pip install -r requirements.txt'
            }
        }

        stage('Dependency Check') {
            steps {
                bat '"C:\\WINDOWS\\py.exe" -m pip list'
            }
        }

        stage('Security Scan') {
            steps {
                bat '"C:\\WINDOWS\\py.exe" -m pip install safety'
                bat '"C:\\WINDOWS\\py.exe" -m safety check'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t smartpark .'
            }
        }

    }
}