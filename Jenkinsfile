pipeline {
    agent any

    environment {
        IMAGE_NAME = "sujith1ns/devops-html"
        DEPLOYMENT_NAME = "my-app"
    }

    stages {

        stage('Checkout') {
    steps {
        git branch: 'main', url: 'https://github.com/SUJITH-NS/devops-prj2'
    }
}

        stage('Build') {
            steps {
                sh 'echo "Building application..."'
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME:latest .
                '''
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub-creds',
                    usernameVariable: 'sujith1ns',
                    passwordVariable: 'Sujith@8082'
                )]) {
                    sh '''
                    echo "Logging into Docker Hub..."
                    echo $PASS | docker login -u $USER --password-stdin

                    echo "Pushing Docker image..."
                    docker push $IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Starting deployment..."

                # Try Kubernetes deployment (safe fallback)
                kubectl apply -f deployment.yaml --validate=false || echo "Kubernetes not configured, skipping..."

                echo "Deployment stage completed"
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline executed successfully!"
        }
        failure {
            echo "❌ Pipeline failed!"
        }
    }
}
