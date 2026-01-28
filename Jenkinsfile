pipeline {
    agent {label 'server1'}
    environment {
        FIRST_NAME = 'Shehryar'
    }
    parameters {
        string(name: 'LAST_NAME', defaultValue: 'Shah')
    }
    tools {maven 'maven'}
    stages {
        stage('build') {
            steps {
                sh 'mvn clean package'
                echo "Hello my name is $FIRST_NAME ${params.LAST_NAME}"
            }
        }
        stage('test') {
            parallel {
                stage ('Test A') {
                    steps {
                        echo 'Running test A'
                    }
                }
                stage ('Test B'){
                    steps {
                        echo 'Running test B'
                    }
                }
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: '**/*.war'
        }
    }
}