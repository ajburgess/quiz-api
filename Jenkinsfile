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

    stage('Create version') {
      steps {
        sh '''export AWS_ACCESS_KEY_ID=99999999
export AWS_SECRET_ACCESS_KEY=ABCD234
'''
        sh '''echo ${AWS_ACCESS_KEY_ID}
echo ${AWS_ACCESS_KEY_ID}'''
        ebCreateApplicationVersion(applicationName: 'quiz-api-ajb', versionLabel: 'FromS3', s3Bucket: 'quiz-api-deploy', s3Key: 'app.zip')
      }
    }

    stage('Deploy to EBS') {
      steps {
        awsebReleaser(credentialId: 'qa-tutor', awsRegion: 'eu-west-2', applicationName: 'quiz-api-ajb', environmentId: 'e-pepkykhj6m', versionLabel: 'Sample Application')
      }
    }

  }
  environment {
    HOME = '.'
  }
}