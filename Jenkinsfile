pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "Building..."'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t sujith1ns/devops-html .'
            }
        }

        stage('Deploy') {
    steps {
        sh '''
        kubectl apply -f deployment.yaml --validate=false
        '''
    }
}
        }
    }
}
