pipeline {
  agent any
  parameters { string(name: 'PROJECTNAME', defaultValue: 'psappp', description: 'This is the OpenShift name of the project to deploy to') }

  stages {
    stage('Compile') {
      steps {
        sh 'echo "Hello World"'
        sh 'echo "This is stage 1 - Compile"'
        sh 'echo "Building ${PROJECTNAME} Version ${currentBuild.number}"'
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
