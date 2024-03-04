pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    sh '/path/to/apache-maven-3.9.6/bin/mvn clean package'
                }
                post {
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
