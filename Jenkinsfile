podTemplate(label: 'agent-pod', containers: [
    containerTemplate(name: 'python', image: 'python:3.7.6', command: 'cat', ttyEnabled: true)
  ]
  ) {
    node('dynamic-jenkins-agent') {
      stages{
        stage('build') {
          container('python') {
            sh 'pip install -r requirements.txt'
          }
        }
        stage('test') {
          container('python') {
            sh 'python test.py'
          }
        }
      }
    }
}