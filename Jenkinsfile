pipeline {
  agent any

  environment {
    DOCKER_CREDENTIALS = credentials('dockerhub-credentials-id') // 도커허브 아이디
  }

  stages {
    stage('Git Clone') {
      steps {
        git url: 'https://github.com/USER/REPO.git', credentialsId: 'github-token-id', branch: 'main'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker-compose build'
      }
    }
    stage('Push Docker Image (옵션)') {
      steps {
        sh 'docker login -u $DOCKER_CREDENTIALS_USR -p $DOCKER_CREDENTIALS_PSW'
        sh 'docker-compose push'
      }
    }
    stage('Deploy Service') {
      steps {
        sh 'docker-compose down'
        sh 'docker-compose up -d --build'
      }
    }
  }
  post {
    failure {
      echo '빌드 또는 배포에 실패했습니다. 담당자에게 알림 전송 등.'
    }
    success {
      echo '성공적으로 배포 완료.'
    }
  }
}
