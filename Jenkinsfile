pipeline {
  agent any
  stages {
    stage('Build Demo App') {
      when {
        expression {
          params.REQUESTED_ACTION == 'Build'
        }

      }
      steps {
        sh '''npm install
npm run build'''
      }
    }
    stage('Test') {
      steps {
        sh 'npm run test'
      }
    }
    stage('Deploy') {
      steps {
        sh '''mkdir playbooks/files
cp nodejs-demoapp.zip playbooks/files/nodejs-demoapp.zip
ansible-playbook playbooks/deploy_dev.yml'''
      }
    }
  }
  when {
        expression {
          params.REQUESTED_ACTION == 'Stage'
        }
      } 
    
  parameters {
    choice(name: 'REQUESTED_ACTION', choices: '''Build
    Stage
''', description: 'Type of action to perform')
  }
}
