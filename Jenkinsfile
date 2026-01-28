pipeline {
    agent {label 'server1'}
    tools {maven 'maven'}
    stages {
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage ('test') {
            steps {
                echo 'Running tests'
                sh 'mvn test'
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: '**/*.war'
        }
    }
}