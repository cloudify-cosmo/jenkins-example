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
        container('node') {
          sh 'pip install -r requirements.txt'
        }
      }
    }
    stage('Run Unit Tests') {
      steps {
        container('docker') {
          sh 'python test.py'
        }   
      }
    }
  }
}