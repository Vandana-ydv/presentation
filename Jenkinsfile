pipeline {
    agent any

    tools {
        // must match the name you gave in Manage Jenkins -> Tools -> SonarQube Scanner
        // remove this block if you didn't configure a named scanner tool
    }

    stages {

        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Clone Repository') {
            steps {
                bat 'git clone https://github.com/yourusername/smart-parking.git temp-clone || echo "Already checked out"'
            }
        }

        stage('Install Dependencies') {
            steps {
                // change this based on your project type
                // for Node.js:
                bat 'npm install'
                // for Python:
                // bat 'pip install -r requirements.txt'
            }
        }

        stage('Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--scan .'
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
                bat 'docker run -d -p 3000:3000 --name smartpark-container smartpark'
            }
        }

    }
}