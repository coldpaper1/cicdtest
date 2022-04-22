pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/coldpaper1/cicdtest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t mhkim1560/testshop:newnewmain .
        sudo docker push mhkim1560/testshop:newnewmain
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kubectl set image deployment deploy-main ctn-main=mhkim1560/testshop:newnewmain
        '''
      }
    }
  }
}
