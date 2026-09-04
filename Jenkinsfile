pipeline {
  agent any

  stages {
    stage('Build') {
      agent {
        docker {
          image 'node:18-alpine'
          reuseNode true
        }
      }
      steps {
        sh '''
          npm ci
          npm run build
        '''
      }
    }

    stage('Test') {
      agent {
        docker {
          image 'node:18-alpine'
          reuseNode true
        }
      }
      steps {
        sh '''
          test -f build/index.html
          npm test
        '''
      }
    }

    stage('Docker Build') {
      steps {
        script {
          dockerImage = docker.build(
            'ihor8nastenko8devops/test-jenkins-pipeline'
          )
        }
      }
    }

    stage('Docker Publish') {
      steps {
        script {
          docker.withRegistry('', 'ihor8nastenko8devops') {
            dockerImage.push()
          }
        }
      }
    }
  }
}
