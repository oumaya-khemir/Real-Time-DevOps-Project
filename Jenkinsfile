pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

   

    stages {
        stage('Git Checkout') {
            steps {
               git branch: 'main', credentialsId: '1d11af70-1826-4476-b412-cf9a8c8e3515', url: 'https://github.com/oumaya-khemir/Real-Time-DevOps-Project.git'
            }
        }
        
        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }
        stage('File System Scan') {
            steps {
                sh "trivy fs --format table -o trivy-fs-report.html ."
            }
        }
    }
}
