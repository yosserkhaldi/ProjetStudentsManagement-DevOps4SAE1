pipeline {
    agent any

    triggers {
        // Pour le TP : Jenkins vérifie toutes les 2 minutes s'il y a un nouveau commit
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-creds-id',
                    url: 'https://github.com/yosserkhaldi/ProjetStudentsManagement-DevOps4SAE1.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -B clean package -DskipTests'
            }
        }

        // Tu pourras réactiver plus tard pour le bonus
        /*
        stage('Tests') {
            steps {
                sh 'mvn test'
            }
        }
        */

        stage('Archive artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
