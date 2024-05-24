pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
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
        stage('SonarQube Analsyis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Real-Time-DevOps-Project -Dsonar.projectKey=Real-Time-DevOps-Project \
                    -Dsonar.java.binaries=. '''
                            
                }
            }
        }
        
       // stage('Quality Gate') {
        //    steps {
           //     script {
          //        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token' 
            //    }
          //  }
       // } 
        //stage('Publish To Nexus') {
          //  steps {
            //   withMaven(globalMavenSettingsConfig: 'global-settings', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
              //      sh "mvn deploy"
              //  }
           // }
       // }
        stage('Build & Tag Docker Image') {
            steps{
               
                sh "docker login -u khemiroumaya -p 171016*+/-"
                sh "docker build -t khemiroumaya/DevOpsProject:latest ."
                sh "docker image push khemiroumaya/DevOpsProject:latest"
                
        
      }

        }
    }
}
