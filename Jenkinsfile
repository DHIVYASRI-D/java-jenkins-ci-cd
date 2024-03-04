pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh "mvn clean package"
                }
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    deploy adapters: [tomcat9(credentialsId: 'c3062dcb-ef1e-40fa-93be-ddb0dcda954b', path: '', url: 'http://localhost:8082/')], contextPath: null, war: '**/*.war'
                }
            }
        }
    }
}
