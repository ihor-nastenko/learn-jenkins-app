pipeline {
  agent {
    docker {
      image 'node:18-alpine'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh '''ls -la
          node --version
          npm --version
          npm ci
          npm run build'''
      }
    }

    stage('Test') {
      steps {
        sh '''test -f build/index.html
npm test'''
      }
    }

    stage('Docker publish') {
      environment {
        registry = 'ihor8nastenko8devops/test-jenkins-pipeline'
        registryCredential = 'ihor8nastenko8devops'
      }
      steps {
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }

      }
    }

  }
}