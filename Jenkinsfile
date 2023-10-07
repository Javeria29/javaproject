pipeline{
    agent any

    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts:'**/target/*.war'
                }
            }

        }
        stage('deploy to tomcat server'){
deploy adapters: [tomcat9(credentialsId: 'b8bbb717-f703-49fd-8350-823535432a5f', path: '', url: 'http://localhost:8081/manager/html/')], contextPath: null, war: '**/*.war'
        }
    }
}
