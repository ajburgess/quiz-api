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
        step([
                              $class: 'AWSEBDeploymentBuilder',
                              credentialId: "qa-tutor",
                              awsRegion: 'eu-west-2',
                              applicationName: 'quiz-api-ajb',
                              environmentName: 'quizapiajb-prod',
                              rootObject: '.',
                              includes: 'package*.json, src/*',
                              excludes: '',
                              bucketName: 'quiz-api-deploy',
                              keyPrefix: '',
                              versionLabelFormat: "V5",
                              versionDescriptionFormat: "V5"
                            ])
        }
      }

    }
    environment {
      HOME = '.'
    }
  }