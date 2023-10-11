pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the GitHub repository
                git url: 'https://github.com/ashoktg012/SaiJavaCode.git', branch: 'master'
            }
        }

        stage('Build docker image') {
            steps {
                script {
                def registry = 'docker.io' // Docker Hub registry
                def customImageName = 'ashoktg012/firstimage1:latest'

                    // Build the Docker image
                    sh "docker build -t $customImageName -f Dockerfile ."

                    // Push the Docker image to Docker Hub
                    withCredentials([usernamePassword(credentialsId: 'ashokdockerhub', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                        sh "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                        sh "docker push $customImageName"
                    }    
                }
            }
                
        }
        // Add more stages as needed
    }
}

