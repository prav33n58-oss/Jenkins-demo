pipeline {
    agent { label 'built-in' }

    stages {
        stage('Build') {
            steps {
                echo "Building on agent: ${env.NODE_NAME}"
                echo "Branch: ${env.BRANCH_NAME}"
            }
        }
        stage('Test') {
            steps {
                echo "Running tests on: ${env.NODE_NAME}"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying from: ${env.NODE_NAME}"
            }
        }
    }
}
