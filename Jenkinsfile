pipeline {
  agent any
  stages {
    stage('Install') {
      steps {
        sh 'bundle install --path vendor/bundle'
      }
    }
    stage('Build') {
      steps {
        sh '''bundle exec jekyll clean
bundle exec jekyll build'''
      }
    }
    stage('Deploy') {
      steps {
        withCredentials([string(credentialsId: 'uberspace_tdo', variable: 'SERVER')]) {
          sh '''
            set +x
            rsync -avz --delete ./_site/* $SERVER
            '''
          }
        }
      }
    }
  }

