pipeline {
    agent any

    stages {
        stage('w/o docker') {
            steps {
                sh '''
                echo 'Hello World'
                ls -la
                touch container-no.txt
                '''
            }
        }
        stage('with docker') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                echo 'wITH dOCKER'
                ls -la
                touch container-YES.txt
                '''
            }
        }
    }
}
