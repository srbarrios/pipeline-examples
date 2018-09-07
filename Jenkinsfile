pipeline {
  agent any
  stages {
    stage('COMPILE') {
      parallel {
        stage('COMPILE') {
          steps {
            build 'qa.build.app'
          }
        }
      }
    }
    stage('TEST') {
      parallel {
        stage('TEST') {
          steps {
            build 'qa.test.app'
          }
        }
      }
    }
    stage('DEPLOY') {
      parallel {
        stage('DEPLOY') {
          steps {
            build 'qa.deploy.app'
          }
        }
      }
    }
  }
  environment {
    env = 'qa'
  }
}
