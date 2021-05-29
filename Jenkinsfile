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
        sh 'zip package*.json src/** archive.zip'
        archiveArtifacts(artifacts: 'archive.zip', onlyIfSuccessful: true)
        sh 'apt install zip'
      }
    }

  }
  environment {
    HOME = '.'
  }
}