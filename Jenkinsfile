pipeline {
  agent {
    docker {
      image 'node:14'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'pwd; ls'
        sh '''npm install
'''
      }
    }

    stage('Test') {
      steps {
        sh 'npm run test'
      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts(artifacts: 'package*.json, src/**', excludes: 'node_modules', onlyIfSuccessful: true)
      }
    }

  }
  environment {
    HOME = '.'
  }
}