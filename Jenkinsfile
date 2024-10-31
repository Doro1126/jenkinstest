pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/Doro1126/jenkinstest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t doro0704/keduitlab:red .
        sudo docker push doro0704/keduitlab:red
        '''
      }
    }
    stage('image pulling') {
      steps {
        sh '''
        ansible node -m shell -a 'sudo docker pull doro0704/keduitlab:red'
        '''
      }
    }
  }
}