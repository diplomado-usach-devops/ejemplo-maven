pipeline {
    agent any

    stages {

        stage('downloadNexus') {
            steps {
                script {
                        sh 'curl -X GET -u admin:Chaki_123_ http://localhost:8081/repository/maven_M3S10/com/devopsusach2020/DevOpsUsach2020/0.0.1/DevOpsUsach2020-0.0.1.jar -O'
                }
            }
        }

        stage('Run') {
            steps {
                script{
                        //sh 'JENKINS_NODE_COOKIE=dontKillMe nohup bash mvnw spring-boot:run &'
                        sh 'JENKINS_NODE_COOKIE=dontKillMe nohup java -jar DevOpsUsach2020-0.0.1.jar &'
                        sh 'sleep 20'
                }
            }
        }
        stage('Testing') {
            steps {
                script{
                        sh "curl -X GET 'http://localhost:8181/rest/mscovid/test?msg=testing'"
                }
            }
        }
        stage("uploadNexus"){
            steps{
                nexusPublisher nexusInstanceId: 'nexus_test',
                nexusRepositoryId: 'maven_M3S10',
                packages: [
                    [
                        $class: 'MavenPackage',
                        mavenAssetList: [
                                [classifier: '', extension: '', filePath: "DevOpsUsach2020-0.0.1.jar"]
                        ],
                        mavenCoordinate: [
                                artifactId: 'DevOpsUsach2020',
                                groupId: 'com.devopsusach2020',
                                packaging: 'jar',
                                version: '1.0.0'
                        ]
                        ]
                ]
                }
        }
    }
}
