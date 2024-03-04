pipeline {
    agent any

    environment {
        TOMCAT_URL = 'http://192.168.0.108:8082'  // Update with your Tomcat server URL
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Maven build
                    def mvnHome = tool 'Maven'
                    bat "${mvnHome}/bin/mvn clean install"
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Maven test
                    def mvnHome = tool 'Maven'
                    bat "${mvnHome}/bin/mvn test"
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Deploy to Tomcat using Cargo plugin
                    def mvnHome = tool 'Maven'
                    bat "${mvnHome}/bin/mvn cargo:redeploy -Pdeploy-to-tomcat -Dcargo.tomcat.url=${env.TOMCAT_URL}"
                }
            }
        }
    }

    post {
        always {
            // Clean up (optional)
            cleanWs()
        }
    }
}
