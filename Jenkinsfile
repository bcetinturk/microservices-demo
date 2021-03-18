pipeline {
  agent none
//check every minute for changes
//  triggers {
//    pollSCM('*/1 * * * *')
//  }
  stages {
    //Build container image
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
        sh "/kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` --destination=artifactory:8081/app:${env.BUILD_ID}"
    } //container
  } //steps
} //stage(build)
    //Test goes here
    //SonarQube goes here
    //Documentation generation goes here
    //Deploy goes here
    //Performance testing goes here
  } //stages
} //pipeline