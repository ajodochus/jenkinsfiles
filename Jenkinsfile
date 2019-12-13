pipeline {
    agent none
    stages {
        stage('Run Tests') {
            parallel {
                stage('Test On thinkpad') {
                    agent {
                        label "master"
                    }
                    steps {
                        bat "calc.exe"
                    }
                    post {
                        always {
                            println "hello thinkpad"
                        }
                    }
                }
                stage('Test On akoya') {
                    agent {
                        label "akoya_medion"
                    }
                    steps {
                        bat "calc.exe"
                    }
                    post {
                        always {
                            println "hello akoya"
                        }
                    }
                }
            }
        }
    }
}
