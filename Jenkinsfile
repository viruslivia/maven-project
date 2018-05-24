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
  }
}
