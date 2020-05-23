void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com//cloudify-cosmo/jenkins-example"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}

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
        container('python') {
          sh 'pip install -r requirements.txt'
          setBuildStatus("Build succeeded xxxx", "SUCCESS");
        }
      }
    }
    stage('Run Unit Tests') {
      steps {
        container('python') {
          sh 'python test.py'
          setBuildStatus("Build succeeded ddd", "SUCCESS");
        }   
      }
    }
  }
  post {
    success {
        setBuildStatus("Build succeeded", "SUCCESS");
    }
    failure {
        setBuildStatus("Build failed", "FAILURE");
    }
  }
}