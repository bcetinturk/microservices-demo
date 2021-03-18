pipeline {
    environment {
        registry = "bcetinturk/adservice"
        registryCredential = 'dockerhub'
    }

    stages {
        stage('Build') {
            agent {
                kubernetes {
                label 'jenkinsrun'
                defaultContainer 'builder'
                yaml """
            kind: Pod
            metadata:
            name: kaniko
            spec:
            containers:
            - name: builder
                image: gcr.io/kaniko-project/executor:debug
                imagePullPolicy: Always
                command:
                - /busybox/cat
                tty: true
            """
                }
            }
            steps {
                script {
                    sh "/kaniko/executor --dockerfile ./src/adservice/Dockerfile --context ./src/adservice --destination=artifactory:8081/adservice:${env.BUILD_ID}"
                } //container
            } //steps
        } //stage(build)
    }
}