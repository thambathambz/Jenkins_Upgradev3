pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f java-tomcat-sample/pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Deploy') {
            steps {
                deploy war: '**/*.war', 
                  contextPath: '/', 
                  container: 'tomcat8x',
                  url: 'http://35.170.192.194:8080/manager/text'

                  
            }
         }
    }
}
