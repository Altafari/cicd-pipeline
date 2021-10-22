pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/Altafari/cicd-pipeline.git', branch: 'main')
      }
    }

    stage('Application Build') {
      steps {
        sh 'scripts/build.sh'
      }
    }

    stage('Tests') {
      steps {
        sh 'scripts/test.sh'
      }
    }

    stage('Docker Image Build') {
      steps {
        sh '''docker build -t omusiiaka/testrepo
 .'''
      }
    }

    stage('Docker Image Publish') {
      steps {
        script {
          withDockerRegistry([ credentialsId: "dockerHub", url: "" ])
          {
            sh  'docker push omusiiaka/testrepo:latest'
            sh  'docker push omusiiaka/testrepo:$BUILD_NUMBER'}
          }

        }
      }

    }
  }