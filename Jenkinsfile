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
        echo 'BRANCH-NAME: ' + env.BRANCH_NAME
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
    stage('After Build 1') {
      steps {
        echo 'FULL ENV: ' + env
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