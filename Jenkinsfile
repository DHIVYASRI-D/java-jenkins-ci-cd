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
                   deploy adapters: [tomcat9(credentialsId: '04d3a370-fb2f-4d44-9f1e-2ce7b11efc64', path: '/manager/text', url: 'http://192.168.10.6/')], contextPath: '/ci-cd-java-app', war: '**/*.war'
                }
            }
        }
    }
}
