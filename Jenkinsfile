pipeline {
    agent any
    environment {
        NEXUS_URL = 'http://13.201.41.95:8081/'
        NEXUS_REPO = 'maven-releases'
        NEXUS_CREDENTIALS_ID = 'nexus-admin'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/PriyeshPandey07/Nexus-Repo-with-Jenkins.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Upload to Nexus') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "http://13.201.41.95:8081/",
                    groupId: 'com.example',
                    version: '1.0.0',
                    repository: "maven-releases",
                    credentialsId: "nexus-admin",
                    artifacts: [
                        [artifactId: 'nexus-demo', classifier: '', file: 'target/nexus-demo-1.0.0.jar', type: 'jar']
                    ]
                )
            }
        }
    }
}
