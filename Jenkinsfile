pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/thomasplade/Ler-f-rentiel.git', credentialsId: 'github-token-parking'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Deploy to Dev') {
            when {
                branch 'develop'
            }
            steps {
                // Script de déploiement pour l'environnement de développement
                sh 'npm run deploy:dev'
            }
        }

        stage('Deploy to Prod') {
            when {
                branch 'main'
            }
            steps {
                // Script de déploiement pour l'environnement de production
                sh 'npm run deploy:prod'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            junit 'target/surefire-reports/**/*.xml'
        }
    }
}
