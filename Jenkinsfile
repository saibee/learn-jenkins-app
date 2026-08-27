pipeline {
    agent any

    environment {
        BUILD_FILE_NAME = 'index.html'
    }

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
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
               '''
            }
        }

        stage ('Test'){
            
             steps {
                echo 'Testing learning app...'

                sh '''
                    test -f build/$BUILD_FILE_NAME
                    npm run build/$BUILD_FILE_NAME
                '''
             }
        }
    }

    post {
        success{
            archiveArtifacts artifacts: 'build/**'
        }
     }
}
