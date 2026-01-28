pipeline {
    agent { label 'server1' }           // default agent for most stages

    environment {
        FIRST_NAME = 'Shehryar'
    }

    parameters {
        choice(
            choices: ['dev'], 
            name: 'select_environment',
            description: 'Choose target environment'
        )
    }

    tools {
        maven 'maven'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }

        stage('Test') {
            parallel {
                stage('Test A') {
                    agent { label 'server1' }   // ← correct place for agent
                    steps {
                        echo 'Running test A on server1'
                        sh 'mvn test'
                    }
                }
                stage('Test B') {
                    agent { label 'server1' }   // ← correct place for agent
                    steps {
                        echo 'Running test B on server1'
                        sh 'mvn test'
                    }
                }
            }
        }

        stage('Deploy') {
            when {
                expression { params.select_environment == 'dev' }
            }
            agent { label 'server1' }           // explicit agent (optional if same as top-level)
            steps {
                dir('webapp/target') {
                    stash name: 'maven-build', includes: '*.war'
                }
                dir('/var/www/html') {
                    unstash 'maven-build'
                    echo 'Deployed webapp.war to /var/www/html – restart your server if needed'
                }
            }
        }
    }

    post {
        success {
            echo "Build & Deploy succeeded for ${env.FIRST_NAME}"
        }
    }
}
