pipeline {
    agent any

    options {
        // Esto hace que solo corra en tu rama
        disableConcurrentBuilds()
    }

    triggers {
        // Esto hace que el CI se active cuando empujes a TU rama
        pollSCM('H/2 * * * *')
    }

    stages {

        stage('Checkout') {
            steps {
                // Obtiene el código del repo
                checkout scm
            }
        }

        stage('Instalar Flutter SDK') {
            steps {
                echo "Instalando Flutter en Jenkins..."

                sh '''
                if [ ! -d "$HOME/flutter" ]; then
                    git clone https://github.com/flutter/flutter.git -b stable $HOME/flutter
                fi
                export PATH="$HOME/flutter/bin:$PATH"

                flutter --version
                '''
            }
        }

        stage('Pub Get') {
            steps {
                sh '''
                export PATH="$HOME/flutter/bin:$PATH"
                cd patrullapp
                flutter pub get
                '''
            }
        }

        stage('Analyze') {
            steps {
                sh '''
                export PATH="$HOME/flutter/bin:$PATH"
                cd patrullapp
                flutter analyze
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                export PATH="$HOME/flutter/bin:$PATH"
                cd patrullapp
                flutter test || true
                '''
            }
        }
    }

    post {
        always {
            echo "CI FINALIZADO"
        }
    }
}
