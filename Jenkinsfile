pipeline {
    agent any
    stages {
        stage('Lint HTML & Dockerfile'){
            steps {
                sh 'tidy -q -e blue-green/blue/*.html'
                sh 'tidy -q -e blue-green/green/*.html'
                sh 'hadolint blue-green/blue/Dockerfile'
                sh 'hadolint blue-green/green/Dockerfile'
            }
        }
        stage('Build and Publish Docker Image'){
            steps{        
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                    def blue = docker.build("ranjitklive/blue-image","-f blue-green/blue/Dockerfile blue-green/blue")
                    def green = docker.build("ranjitklive/green-image","-f blue-green/green/Dockerfile blue-green/green")
                    blue.push()
                    green.push()    
                    }
                }
            }
        }
    }
}
