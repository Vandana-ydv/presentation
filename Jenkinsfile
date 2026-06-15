pipeline {
    agent any

    

    stages {

        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Clone Repository') {
            steps {
                bat 'echo Repository already checked out via SCM'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'py -m pip install -r requirements.txt'
            }
        }

       stage('Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--scan .', odcInstallation: 'DP-Check'
                dependencyCheckPublisher()
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    bat 'sonar-scanner -Dsonar.projectKey=smart-parking -Dsonar.sources=.'
                }
            }
        }

        stage('Trivy Scan') {
            steps {
                bat 'trivy fs .'
            }
        }

        stage('Check Docker') {
            steps {
                bat 'docker --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t smartpark .'
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker tag smartpark yourdockerhubusername/smartpark:latest'
                bat 'docker push yourdockerhubusername/smartpark:latest'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker stop smartpark-container || exit 0'
                bat 'docker rm smartpark-container || exit 0'
                bat 'docker run -d -p 5000:5000 --name smartpark-container smartpark'
            }
        }

    }
}