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
        sh 'docker build -t testrepo .'
        sh 'docker tag testrepo omusiiaka/testrepo:latest'
        sh 'docker tag testrepo omusiiaka/testrepo:$BUILD_NUMBER'
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
