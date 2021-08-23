pipeline {
  agent any
  parameters {
    string(name: 'projectName', defaultValue: 'psapp', description: 'Project name to create or target for update')
    choice(name: 'EXISTING', choices: ['yes'], defaultValue: 'yes', description: 'Does Moodle database already exist?')
  }

  stages {
    stage('Create project') {
    steps {
        sh """cd openshift
oc login https://localhost:8443 --username developer --password developer --insecure-skip-tls-verify=true
if ! oc project ${projectName}
then
  oc new-project ${projectName}
fi"""
      }
    }
    stage('Build add or update Moodle configuration') {
      steps {
        sh """cd openshift
oc login https://localhost:8443 --username developer --password developer --insecure-skip-tls-verify=true
oc project ${projectName}
oc apply -f moodle-imagestream.yaml
oc apply -f moodle-build.yaml
oc apply -f moodle-data-persistentvolumeclaim.yaml
oc apply -f moodle-service.yaml
oc apply -f moodle-route.yaml || echo 'Route already in place'"""
        }
    }
    stage('Build moodle image') {
      steps {
        sh """oc login https://localhost:8443 --username developer --password developer --insecure-skip-tls-verify=true
oc start-build moodle"""
      }
    }
    stage('Deploy PetcClinic Container To Openshift') {
      steps {
        sh """cd openshift
oc login https://localhost:8443 --username developer --password developer --insecure-skip-tls-verify=true
oc project ${projectName}
oc apply -f moodle-deploymentconfig.yaml"""
      }
    }
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
