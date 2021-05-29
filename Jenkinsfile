pipeline {
  agent {
    docker {
      image 'node:14'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh '''node --version
npm --version
whoami
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