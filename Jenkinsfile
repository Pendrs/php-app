pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Pendrs/php-app' // ganti dengan repo Anda
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'composer install'
            }
        }

        stage('Unit Test') {
            steps {
                sh './vendor/bin/phpunit'
            }
            post {
                success {
                    echo '✅ Test berhasil!'
                }
                failure {
                    echo '❌ Test gagal!'
                }
            }
        }

        stage('Deploy Docker Image') {
            steps {
                sh 'docker build -t php-app:latest .'
                sh 'docker run -d -p 8000:8000 php-app:latest'
            }
        }
    }
}
