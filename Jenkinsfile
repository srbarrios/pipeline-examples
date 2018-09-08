pipeline {
  agent any
  stages {
    stage('COMPILE') {
      steps {
        echo 'Building..'
        build 'QA/qa.build.app'
        ansiColor('xterm') {
              echo "\u001B[31mI'm Red\u001B[0m Now not"
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
      when {
        // skip this stage unless on Master branch
        branch "master"
      }
      
      steps {
        echo 'Deploying....'
        build 'QA/qa.deploy.app'
      }
      
      post {
        aborted {
          echo "Stage 'DEPLOY' WAS ABORTED"
        }
        always {
          echo "Stage 'DEPLOY' finished"
        }
        changed {
          echo "Stage 'DEPLOY' HAVE CHANGED"
        }
        failure {
          echo "Stage 'DEPLOY' FAILED"
        }
        success {
          echo "Stage 'DEPLOY' was Successful"
        }
        unstable {
          echo "Stage 'DEPLOY' is Unstable"
        }
      }
    }
  }
  environment {
    env = 'qa'
  }
}
