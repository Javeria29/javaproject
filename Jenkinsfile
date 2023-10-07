pipeline{
    agent any
    tools{
        maven 'local_maven'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
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
                script {
                    def server = tomcat9(
                        credentialsId: 'b8bbb717-f703-49fd-8350-823535432a5f',
                        path: '',
                        url: 'http://localhost:8081/manager/html/'
                    )
                    def warFile = findFiles(glob: '**/*.war')[0]
                    server.deploy contextPath: null, war: warFile
                }
            }
        }
    }
}
