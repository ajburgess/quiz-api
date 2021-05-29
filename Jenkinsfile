pipeline {
  agent {
    dockerfile {
      filename 'xyz.docker'
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
      }
    }

  }
  environment {
    HOME = '.'
  }
}