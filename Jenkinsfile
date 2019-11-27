pipeline {
    agent any
    
  stages {

    stage('Git-Checkout') {
      steps {
        echo "Checking out from Git Repo";
        git 'https://github.com/prathap87/prathap1.git'
      }
    }

    stage('Deploy') {
      steps {
        echo "Deploying the build";
        bat label: '', script: 'Deploy.bat'
      }
    }

    stage('Quality check') {
      steps {
        echo "Running Quality check";
        bat label: '', script: 'Quality.bat'
      }
    }
  
  stage('Security check') {
      steps {
        echo "Running security check";
        bat label: '', script: 'security.bat'
      }
    }

  }

  post {
    success {
      echo "SUCCESS"
    }
    failure {
      echo "FAILURE"
    }
    changed {
      echo "Status Changed: [From: $currentBuild.previousBuild.result, To: $currentBuild.result]"
    }
    always {
      script {
        def result = currentBuild.result
        if (result == null) {
          result = "SUCCESS"
        }
      }
    }
  }
}
