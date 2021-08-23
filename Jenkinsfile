pipeline {
  agent any
  parameters {
    string(name: 'projectName', defaultValue: 'psapp', description: 'Project name to create or target for update')
  }

  stages {
    
        stage('Set Moodle Deploy Existing or New') {
      steps {
        sh """cd openshift  
      oc login https://localhost:8443 --username developer --password developer --insecure-skip-tls-verify=true
      oc project ${projectName}
      oc set env dc/moodle MOODLE_SKIP_INSTALL=yes
        """
      }
    }
  }
}
