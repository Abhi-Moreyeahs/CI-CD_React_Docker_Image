pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_VERSION = '3.8'
    }

    stages {
        stage('Build') {
            steps {
                // Checkout the code from GitHub
                git 'https://github.com/Abhi-Moreyeahs/CI-CD_React_Docker_Image.git'
            }
        }

        stage('Build and Push Docker Images') {
            steps {
                // Login to your Docker registry (replace with your credentials)
                withCredentials([usernamePassword(credentialsId: '0b258102-2cf5-4ddd-bd92-f55cefd11e12', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                }

                // Build and tag the Docker images
                sh "docker-compose -f docker-compose.yml build"

                // Push the Docker images to your Docker registry (replace with your registry URL)
                sh "docker-compose -f docker-compose.yml push"
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the Docker Compose stack
                sh "docker-compose -f docker-compose.yml up -d"
            }
        }
    }

    // post {
    //     always {
    //         // Clean up
    //         sh "docker-compose -f docker-compose.yml down"
    //     }
    }
