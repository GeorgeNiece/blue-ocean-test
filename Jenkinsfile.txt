pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'npm install'
      }
    }
    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        echo './jenkins/scripts/test.sh'
      }
    }
    stage('Deliver') {
      steps {
        echo './jenkins/scripts/deliver.sh'
      }
    }
    stage('Input') {
      steps {
        input 'Finished using the web site? (Click "Proceed" to continue)'
      }
    }
    stage('') {
      steps {
        echo './jenkins/scripts/kill.sh'
      }
    }
  }
  environment {
    Image = '-p 3000:3000'
  }
}