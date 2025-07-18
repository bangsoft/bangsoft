pipeline {
  agent any

  stages {
    stage('Git Clone') {
      steps {
        git branch: 'deploy', url: 'https://github.com/bangsoft/bangsoft.git', credentialsId: 'real-key'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker-compose build'
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
