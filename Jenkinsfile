pipeline {
    environment {
        registry = "bcetinturk/adservice"
        registryCredential = 'dockerhub'
    }

    agent any

    stages {
        stage('Building image') {
            steps{
            script {
                docker.build(registry + ":$BUILD_NUMBER", "-f ./src/adservice/Dockerfile ./src/adservice")
            }
            }
        }
    }
}