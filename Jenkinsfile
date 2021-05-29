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

    stage('Upload to S3') {
      steps {
        withAWS(credentials: 'qa-tutor') {
          s3Upload(bucket: 'quiz-api-deploy', file: 'app.zip')
        }

      }
    }

    stage('Deploy to EBS') {
      steps {
        withAWS(credentials: 'qa-tutor') {
          ebCreateApplicationVersion(s3Bucket: 'quiz-api-deploy', versionLabel: 'V2', applicationName: 'quiz-api-ajb', s3Key: 'app.zip')
        }

      }
    }

  }
  environment {
    HOME = '.'
  }
}