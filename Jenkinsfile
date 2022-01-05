pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                script {
                        sh './mvnw clean compile -e'
                }
            }
        }
        stage('Test') {
            steps {
                script{
                        sh './mvnw clean test -e'
                }
            }
        }
        stage('Jar') {
            steps {
                script{
                        sh './mvnw clean package -e'
                }
            }
        }
        stage('Run') {
            steps {
                script{
                        sh 'JENKINS_NODE_COOKIE=dontKillMe nohup bash mvnw spring-boot:run &'
                }
            }
        }
        stage('Testing') {
            steps {
                script{
                        sh "curl -X GET 'http://localhost:8081/rest/mscovid/test?msg=testing'"
                }
            }
        }
    }
}
