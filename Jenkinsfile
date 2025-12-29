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
                    ls -la
                    mkdir -p build
                    touch build/test.txt
                '''
            }
        }
        stage('Testing') {
            parallel {
                agent {
                        docker {
                            image 'node:18-alpine'
                            reuseNode true
                        }
                    }
                stage('Test-01') {
                    steps {
                        sh '''
                            test -f build/test.txt
                        '''
                    }
                }
                stage('Test-02') {
                    steps {
                        sh '''
                            test -f build/test.txt
                        '''
                    }
                }
            }
        }
    }
    post {
        always {
            sh 'ls -la'
        }
    }    
}
