pipeline {
    agent any

    environment {
        PASS = credentials('Name')
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
                    mkdir -p build
                    touch build/test.txt
                '''
                script {
                    // env.MY_VAR = sh(script: 'date' , returnStdout: true)
                    env.MY_VAR = 'test'
                }
                input 'Proceed to testing?'
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
                            echo "my var is ${env.MY_VAR}"
                            echo $PASS
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
    }
    post {
        always {
            sh 'ls -la'
        }
    }    
}
