String awx_template1 = 'Promote Vault HA'
String awx_template2 = 'Synchronize Vault HA DRP'

properties([parameters([choice(choices: [awx_template1, awx_template2], name: 'template')])])

 
pipeline {
  agent any
  environment {
    EXTRA_VARS = ""
  }
  stages {
    stage('Debug') {
      steps {
        script {
          if (template == awx_template1) {
            env.EXTRA_VARS = "vault_cluster: 'vault_cluster_drp'"
          }
        }
        echo "$template"
        echo env.EXTRA_VARS
      }
    }
    stage('Trigger AWX') {
      steps {
        ansibleTower jobTemplate: "$template",
          extraVars: env.EXTRA_VARS,
          jobType: 'run',
          throwExceptionWhenFail: false,
          towerCredentialsId: 'AWX',
          towerLogLevel: 'full',
          towerServer: 'AWX'
      }
    }
  }
}