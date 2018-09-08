pipeline {
  agent any
  
  //options {
    // using the Timestamper plugin we can add timestamps to the console log
    //timestamps() <--- BUG: https://issues.jenkins-ci.org/browse/JENKINS-48556
  //}
  
  environment {
    env = 'qa'
  }
  
  stages {
    stage('Build') {
      steps {
        echo 'Building..'
        build 'QA/qa.build.app'
        ansiColor('xterm') {
              echo "\u001B[31mI'm Red\u001B[0m Now not"
        }
      }
    }
    stage('Test') {
      steps {
        echo 'Testing..'
        build 'QA/qa.test.app'
      }
    }
    stage('Deploy') {
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
          echo "Stage 'Deploy' WAS ABORTED"
        }
        always {
          echo "Stage 'Deploy' finished"
        }
        changed {
          echo "Stage 'Deploy' HAVE CHANGED"
        }
        failure {
          echo "Stage 'Deploy' FAILED"
        }
        success {
          echo "Stage 'Deploy' was Successful"
        }
        unstable {
          echo "Stage 'Deploy' is Unstable"
        }
      }
    }
  }
  
  post {
    failure {
      // notify users when the Pipeline fails
      mail to: 'oscar.barrios@gmail.com',
          subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
          body: "Something is wrong with ${env.BUILD_URL}"
    }
  }
  
}
