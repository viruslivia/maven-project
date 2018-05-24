pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
      post {
        success {
          echo 'Now archiving the package...'
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }
    
    stage('Deploy to Staging') {
      steps {
        build job: 'deploy'
      }
    }
    
    stage('Deploy to Production') {
      steps {
        timeout(time:5, unit: 'DAYS') {
          input message: 'Approve PRODUCTION deployment?'
        }
        
        build job: 'deploy-to-prod'
      }
      post {
        success {
          echo 'Successfully deployed to Production'
        }
        failure {
          echo 'The deployment to production failed'
        }
      }
    }
  }
}
