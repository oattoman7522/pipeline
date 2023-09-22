properties([parameters([choice(choices: ['Promote Vault HA', 'Synchronize Vault HA DRP', 'testjenkins'], name: 'template')])])

pipeline {
  agent any
  stages {
    stage('101') {
      steps {
        echo "Pran"
        echo "$template"
      }
    }
    stage('awx') {
      steps {
        ansibleTower(
              towerServer: 'AWX',  // set server on AWX tower
              towerCredentialsId: 'AWX',     // User and password
              templateType: 'job',        // template type
              jobTemplate: "$template",
              towerLogLevel: 'full',
              verbose: true,
        )      
      }
    }
  }
} 
