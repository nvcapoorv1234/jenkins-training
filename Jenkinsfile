pipeline {
  agent	any

  stages {
    stage('Compile') {
      steps {
       	sh 'echo "Hello	World"'
       	sh 'echo "This is stage	1 - Compile"'
      }
    }
    stage('Test') {
      steps {
       	sh 'echo "Now we are testing the code"'
      }
    }
    stage('Publish artifact') {
      steps {
       	sh 'ls /tmp'
       	sh 'echo "Artifact published"'
      }
    }
  }
}
