pipeline {
    agent any
    
  stages {

    stage('Git-Checkout') {
      steps {
        echo "Checking out from Git Repo";
        git 'https://github.com/asha-afzal/pipeline.git'
      }
    }

    stage('Build') {
      steps {
        echo "Building the checked out project";
        bat label: '', script: 'Build.bat'
      }
    }

    stage('Unit') {
      steps {
        echo "Running unit test";
        bat label: '', script: 'Unit.bat'
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
