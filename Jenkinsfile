@Library("jenkins-shared-library@main") _

pipeline {
    agent {
        docker {
            image 'python:3.11-slim'
            args '--user root'
        }
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Checking out branch: ${env.BRANCH_NAME}"
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests with coverage...'
                sh 'pytest test_app.py --cov=app --cov-report=term-missing -v'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Bandit security scan...'
                sh 'bandit -r app.py -ll'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging application...'
                sh 'zip -r app-${BUILD_NUMBER}.zip app.py requirements.txt'
            }
        }

        stage('Archive') {
            steps {
                echo 'Archiving artifact...'
                archiveArtifacts artifacts: "app-${BUILD_NUMBER}.zip", fingerprint: true
            }
        }

    }

    post {
        success {
            echo "Pipeline passed! Artifact: app-${BUILD_NUMBER}.zip"
        }
        failure {
            echo 'Pipeline failed — check the stage that went red.'
        }
    }
}
