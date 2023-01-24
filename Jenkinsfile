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
                script {
                    def server = "http://tomcat_host:9090"
                    def artifact = fingerprint('**/*.war')
                    def deployPath = "${artifact.fileName}"
                    def credentialsId = "tomcat_credentials"
                    sh "curl --upload-file ${deployPath} ${server}/deploy?path=/${deployPath} --user ${credentialsId}"
                }
            }
        }
    }
}
