pipeline {
    agent any
    stages {

        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Sriramya', url: 'https://github.com/SriramyaGanni/JavaMaven_Web_Project.git']])
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t food-webapp .'
            }
        }

        stage('Docker Run') {
            steps {
                sh 'docker rm -f food-container || true'
                sh 'docker run -d -p 4003:8080 --name food-container food-webapp'
            }
        }
    }
}
