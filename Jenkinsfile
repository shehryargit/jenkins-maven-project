pipeline {
    agent none

    stages {
        stage('Build') {
            agent any
            steps {
                echo 'This is a build step'
            }
        }

        stage('Test') {
            agent any
            steps {
                echo 'This is a test step'
            }
        }

        stage('Deploy') {
            agent any
            steps {
                echo 'This is a deploy step'
            }
        }
    }
}
