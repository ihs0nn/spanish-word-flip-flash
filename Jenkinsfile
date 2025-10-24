pipeline {
    agent any

    options {
        ansiColor('xterm')
    }

    stages {
        stage('Build') {
            agent {
                docker{
                    image 'node:22-alpine'
                }
            }
            steps{
                sh "npm ci"
                sh "npm run build"
            }
        }
        stage('test'){
            parallel {
                stage('unit test') {
                    agent {
                        docker{
                            image 'node:22-alpine'
                            reuseNode true
                        }
                    }
                    steps{
                        //Unit tests with vitest
                        sh "npx vitest run --reporter=verbose"
                    }
                }
            }
        }
        stage('deploy'){
            agent {
                docker{
                    image 'alpine'
                }
            }
            steps{
                //Mock deployement which does nothing
                echo 'Mock deployement was successful!'
            }
        }
    }
}