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
        sh '''zip app.zip package*.json
cd src
zip ../app.zip -r *'''
        archiveArtifacts(artifacts: 'app.zip', onlyIfSuccessful: true)
      }
    }

  }
  environment {
    HOME = '.'
  }
}