pipeline {
    agent any

    environment {
        TOMCAT_URL = 'http://192.168.0.108:8082/'
        TOMCAT_CREDENTIALS_ID = 'c3062dcb-ef1e-40fa-93be-ddb0dcda954b'
        CONTEXT_PATH = 'your-context-path'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Your build steps here
                    // For example: sh 'mvn clean install'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    deploy adapters: [tomcat9(credentialsId: TOMCAT_CREDENTIALS_ID, path: '', url: TOMCAT_URL)], contextPath: CONTEXT_PATH, war: '**/*.war'
                }
            }
        }
    }
}
