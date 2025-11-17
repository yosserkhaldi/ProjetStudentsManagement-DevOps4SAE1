pipeline {
    agent any

    tools {
        // Noms EXACTS comme dans Manage Jenkins > Global Tool Configuration
        maven 'Maven-3.6.3'
        jdk   'JDK17'
    }

    triggers {
        // Option 1 : Poll SCM toutes les 2 minutes (facile en local)
        pollSCM('H/2 * * * *')
        // Option 2 si tu arrives à configurer un webhook GitHub :
        // githubPush()
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
                sh 'mvn -B clean package'
            }
        }

        stage('Tests') {
            steps {
                sh 'mvn tst'
            }
        }

        stage('Archive artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
