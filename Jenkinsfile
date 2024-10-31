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
    stage('ansible command') {
      steps {
        sh '''
        ansible master -m shell -a 'sudo kubectl create deploy web-red --replicas=3 --port=80 --image=doro0704/keduitlab:red'
        ansible master -m shell -a 'sudo kubectl expose deploy web-red --type=LoadBalancer --port=80 target-port=80 --name=web-red-svc'
        '''
      }
    }
  }
}