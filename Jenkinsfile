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
      echo 'branch name: ' + env.BRANCH_NAME
      echo 'CHANGE_ID: ' + env.CHANGE_ID
      echo 'Full env ' + env
      steps {
        container('python') {
          sh 'pip install -r requirements.txt'
        }
      }
    }
    stage('Run Unit Tests') {
      steps {
        container('python') {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh 'python test.py'
          }
        }   
      }
    }
    stage('After Build 1') {
      steps {
        container('python') {
          sh 'echo "Hello world"'
        }   
      }
    }
    stage('After Build 2') {
      steps {
        container('python') {
          sh 'echo "Hello world 2"'
        }   
      }
    }
    stage('After Build 3') {
      steps {
        container('python') {
          sh 'echo "Hello world 3"'
        }   
      }
    }
  }
}