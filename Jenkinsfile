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
        sudo docker build -t mhkim1560/testshop:newnewblog .
        sudo docker push mhkim1560/testshop:newnewblog
        '''
      }
    }
    stage('index change') {
      steps {
        sh '''
        sudo chmod +x exec.sh
        sudo ./exec.sh
	...
      }
    }
    stage('docker build and push2') {
      steps {
        sh '''
        sudo docker build -t mhkim1560/testshop:newnewshop .
        sudo docker push mhkim1560/testshop:newnewshop
        ...
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kubectl set image deployment deploy-main ctn-blog=mhkim1560/testshop:newnewblog
        sudo kubectl set image deployment deploy-main ctn-shop=mhkim1560/testshop:newnewshop 
        '''
      }
    }
  }
}
