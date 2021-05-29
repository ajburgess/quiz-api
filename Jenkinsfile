pipeline {
  agent any
  stages {
    stage('Build') {
      agent {
        docker {
          image 'node:14'
        }

      }
      steps {
        sh '''npm install
'''
      }
    }

    stage('Test') {
      steps {
        sh 'npm run test'
      }
    }

  }
}