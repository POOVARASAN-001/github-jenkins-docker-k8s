
pipeline {
    agent any

    environment {
        DOCKER = 'D:\\DockerApp\\resources\\bin\\docker.exe'
        KUBECTL = 'D:\\DockerApp\\resources\\bin\\kubectl.exe'
        KUBECONFIG = 'C:\\Users\\POOVARASAN\\.kube\\config'
        IMAGE = 'final-cicd-app:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub by Jenkins SCM.'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '"%DOCKER%" build -t %IMAGE% .'
            }
        }

        stage('Test') {
            steps {
                bat '"%DOCKER%" run --rm %IMAGE% nginx -t'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat '"%KUBECTL%" apply --validate=false -f deployment.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat '"%KUBECTL%" rollout status deployment/final-cicd-app --timeout=120s'
                bat '"%KUBECTL%" get deployments'
                bat '"%KUBECTL%" get pods'
                bat '"%KUBECTL%" get services'
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output for details.'
        }
    }
}
