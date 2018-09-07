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
        stage('') {
          steps {
            build 'prod.compile.app'
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
        stage('') {
          steps {
            build 'prod.test.app'
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
        stage('') {
          steps {
            build 'prod.deploy.app'
          }
        }
      }
    }
  }
  environment {
    env = 'qa'
  }
}