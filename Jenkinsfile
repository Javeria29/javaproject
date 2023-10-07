pipeline {
    agent any
    tools {
        // Use the configured Maven tool name here
        maven 'local_maven'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    // Check if the agent is running on a Unix-like system
                    if (isUnix()) {
                        sh 'mvn clean package'
                    } else {
                        bat 'mvn clean package'
                    }
                }
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Tomcat Server') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'b8bbb717-f703-49fd-8350-823535432a5f', path: '', url: 'http://localhost:8081/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
