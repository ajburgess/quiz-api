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
        sh 'zip archive.zip package*.json src/**/*'
        archiveArtifacts(artifacts: 'archive.zip', onlyIfSuccessful: true)
      }
    }

  }
  environment {
    HOME = '.'
  }
}