pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Checkout the code from GitHub
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/Abhi-Moreyeahs/CI-CD_React_Docker_Image.git']]])

                // Build the Docker image
                script {
                    def dockerImage
                    def dockerImageName = "my-react-app"  // Replace with your desired Docker image name
                    def dockerTag = "${dockerImageName}:${env.BUILD_NUMBER}"

                    // Build the React app inside the Docker image using the provided Dockerfile
                    dockerImage = docker.build(dockerTag, "-f Dockerfile .")
                }
            }
        }
        stage('Deploy') {
            steps {
                // Push the Docker image to a registry (optional)
                script {
                    def dockerRegistryUrl = "https://hub.docker.com/r/abhishekkr3110/react_image"  // Replace with your Docker registry URL
                    def dockerCredentialsId = "docker-hub-credentials"  // Replace with your Jenkins Docker credentials ID

                    // Push the Docker image to the specified registry
                    docker.withRegistry(dockerRegistryUrl, dockerCredentialsId) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}