pipeline {

  agent any

  stages {

    stage('Source') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'Building stage!'
        sh 'make build'
      }
    }

    stage('Unit tests') {
      steps {
        sh 'make test-unit'
        archiveArtifacts artifacts: 'results/*.xml'
      }
    }

    stage('API tests') {
      steps {
        sh 'make test-api'
        archiveArtifacts artifacts: 'results/*.xml'
      }
    }

    stage('E2E tests') {
      steps {
        sh 'make test-e2e'
        archiveArtifacts artifacts: 'results/*.xml'
      }
    }
  }

  post {
    always {
      junit 'results/*_result.xml'
      cleanWs()
    }
  }
}
