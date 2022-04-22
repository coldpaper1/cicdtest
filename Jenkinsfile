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
        sudo docker build -t mhkim1560/testshop:newnewblog1 .
        sudo docker push mhkim1560/testshop:newnewblog1
        '''
      }
    }
    stage('index change') {
      steps {
        sh '''
        sudo sed 's/BLOG/SHOP/' index.html        
	'''
      }
    }
    stage('docker build and push2') {
      steps {
        sh '''
        sudo docker build -t mhkim1560/testshop:newnewshop1 .
        sudo docker push mhkim1560/testshop:newnewshop1
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kubectl set image deployment deploy-blog ctn-blog=mhkim1560/testshop:newnewblog1
        sudo kubectl set image deployment deploy-shop ctn-shop=mhkim1560/testshop:newnewshop1
        '''
      }
    }
  }
}
