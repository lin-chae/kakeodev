pipeline {
  agent any
  stages {
    stage('깃 업데이트') {
      steps {
        git url: 'https://github.com/lin-chae/kakaodevpipeline.git', branch: 'main'
      }
    }

    stage('도커 이미지 빌드 및 푸시') {
      steps {
        sh '''
        sudo docker build -t chaechae121/kakaodev:yellow .
        sudo docker push chaechae121/kakaodev:yellow
        '''
      }
    }

    stage('쿠버네티스 디플로리 서비스') {
      steps {
        sh '''
        ssh 211.183.3.100 'kubectl create deploy deploy-yellow --image=chaechae121/kakaodev:yellow'
        ssh 211.183.3.100 'kubectl expose deploy deploy-yellow --type=NodePort --port=8004 --target-port=80 --name=deploy-yellow-np'
        '''
      }
    }

  }
}
