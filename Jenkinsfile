pipeline {
  agent any
  stages {
    stage('Build') {
      agent {
        docker {
          image 'node:18-alpine'
          args '-p 3000:3000'
        }

      }
      steps {
        sh '''ls -la
node --version
npm --version'''
      }
    }

  }
}