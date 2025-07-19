pipeline {
  agent any

  stages {
    stage('Checkout Source') {
      steps {
        git branch: 'deploy', url: 'https://github.com/bangsoft/bangsoft.git', credentialsId: 'github-app'
      }
    }

    stage('Clean & Rebuild Containers') {
      steps {
        sh 'docker-compose down --rmi all --volumes --remove-orphans'
        sh 'docker-compose build --no-cache'
        sh 'docker-compose up -d'
      }
    }
  }

  post {
    success {
      echo '✅ 배포 성공!'
    }
    failure {
      echo '🚨 빌드 또는 배포 실패. 담당자에게 알림 전송 가능'
    }
  }
}
