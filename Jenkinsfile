pipeline {
    agent {
        docker 'gcc/latest'
    }
    stages {
        stage('prebuild') {
            echo 'It is running'
        }
        stage('build') {
            sh 'make'
        }
        stage('artifactory') {
            def server = Artifactory.newServer url: 'http://192.168.18.181:8081', username: 'enc_encoder', password: 'tfidm2018'
            def uploadSpec = """{
            "files": [
                {
                "pattern": "hello_exec",
                "target": "enc_encoder/c_test"
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