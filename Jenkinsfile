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
                stage('Test-01') {
                    agent {
                        docker {
                            image 'node:18-alpine'
                            reuseNode true
                        }
                    }
                    steps {
                        sh '''
                            test -f build/test.txt
                        '''
                    }
                }
                stage('Test-02') {
                    agent {
                        docker {
                            image 'node:18-alpine'
                            reuseNode true
                        }
                    }
                    steps {
                        sh '''
                            test -f build/test.txt
                        '''
                    }
                }
            }
        }
    post {
        always {
            ls -la
        }
    }
}
}
