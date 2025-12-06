pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Flutter Installation') {
            steps {
                bat 'flutter --version'
            }
        }

        stage('Pub Get') {
            steps {
                bat 'flutter pub get'
            }
        }

        stage('Analyze') {
            steps {
                bat 'flutter analyze'
            }
        }

        stage('Tests') {
            steps {
                bat 'flutter test'
            }
        }
    }

    post {
        always {
            echo 'CI FINALIZADO'
        }
    }
}
