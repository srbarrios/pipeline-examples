pipeline {
  agent any
  stages {
    stage('COMPILE') {
      steps {
        echo 'Building..'
        build 'QA/qa.build.app'
        ansiColor('xterm') {
              // Just some echoes to show the ANSI color.
              stage "\u001B[31mI'm Red\u001B[0m Now not"
        }
      }
    }
    stage('TEST') {
      steps {
        echo 'Testing..'
        build 'QA/qa.test.app'
      }
    }
    stage('DEPLOY') {
      steps {
        echo 'Deploying....'
        build 'QA/qa.deploy.app'
      }
    }
  }
  environment {
    env = 'qa'
  }
}
