pipeline {
    agent none

    stages {
        stage('Build') {
            agent any
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
