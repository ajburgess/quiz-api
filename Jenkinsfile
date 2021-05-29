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
        sh '''sudo chown -R 1001:1001 "/.npm"
npm install
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