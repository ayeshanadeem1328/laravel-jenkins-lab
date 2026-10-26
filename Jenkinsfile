pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'COMPOSER_MAX_PARALLEL_HTTP=1 COMPOSER_PROCESS_TIMEOUT=1200 composer install --prefer-dist --no-interaction'
            }
        }

        stage('Configure Laravel') {
            steps {
                sh '''
                    cp .env.example .env
                    touch database/database.sqlite
                    php artisan key:generate
                    php artisan migrate --force
                '''
            }
        }

        stage('Test Laravel') {
            steps {
                sh 'php artisan test'
            }
        }
    }
}
