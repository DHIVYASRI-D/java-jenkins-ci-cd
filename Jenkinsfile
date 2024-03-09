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
                    deploy adapters: [tomcat9(credentialsId: '5d741c1c-b993-425b-a724-4f42d2defe28', path: '/manager/html', url: 'http://localhost:8082/')], contextPath: null, war: '**/*.war'
                    // def tomcatUrl = 'http://192.168.0.108:8082/'
                    // def path = '/manager/html'
                    // def credentials = 'admin:admin'
                    // def warFile = '**/*.war'

                    // sh "curl -v --upload-file ${warFile} -u ${credentials} ${tomcatUrl}/manager/html/deploy?path=${path}"
                }
            }
        }
    }
}
