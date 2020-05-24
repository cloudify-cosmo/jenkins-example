pipeline {
  agent {
    kubernetes {
      label 'ci'
      defaultContainer 'jnlp'
      yamlFile 'build-pod.yaml'
    }
  }
  stages {
    stage('Build') {
      steps {
        echo 'BRANCH NAME: ' + env.BRANCH_NAME
        container('python') {
          sh 'pip install -r requirements.txt'
        }
      }
    }
    stage('Run Unit Tests') {
      steps {
        echo 'CHANGE_ID: ' + env.CHANGE_ID
        container('python') {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh 'python test.py'
          }
        }   
      }
    }
    stage('Run RPMS') {
      steps {
        echo 'ALL ENV:'
        echo sh(returnStdout: true, script: 'env')
        container('python') {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh "exit 1"
          }
        }   
      }
    }
    stage('Run flake8') {
      echo 'CHANGE_URL: ' + env.CHANGE_URL
      steps {
        container('python') {
          sh 'echo "Run flake8"'
        }   
      }
    }
    stage('Check for compatability with python 3') {
      echo 'CHANGE_TITLE: ' + env.CHANGE_TITLE
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh "exit 1"
        }
      }
    }
  }
}