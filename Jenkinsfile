pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'YOUR_GITHUB_REPO_LINK'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Dependency Check') {
            steps {
                stage('Dependency Check') {
    steps {
        bat 'pip list'
    }
}
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t myproject .'
            }
        }

        stage('Run Security Scan') {
            steps {
                bat 'npm audit'
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker tag myproject YOUR_DOCKER_USERNAME/myproject'
                bat 'docker push YOUR_DOCKER_USERNAME/myproject'
            }
        }
    }
}