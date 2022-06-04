pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }
        stage('Deploy Tomcat on Dev Environment'){
            steps {
                sh "Hello World!"
                sh "docker run --rm -p 8081:8080 tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }
    }
}
