pipeline {
    agent {
        docker {
            image 'gcc:latest'
        }
    }
    stages {
        stage('prebuild') {
            steps {
                echo 'hello world'
            }    
        }
        stage('build') {
            steps {
                sh 'make'
            }    
        }
        stage('artifactory') {
            steps {
                script {
                    def server = Artifactory.server 'localhost'
                    def uploadSpec = """{
                    "files": [
                        {
                        "pattern": "hello_exec",
                        "target": "enc_encoder"
                        }
                    ]
                    }"""
                    def buildInfo = Artifactory.newBuildInfo()
                    buildInfo.name = 'test'
                    buildInfo.number = 'v1.2.3'
                    server.upload spec: uploadSpec, buildInfo: buildInfo
                    server.publishBuildInfo buildInfo
                }
            }
        }
    }
}
