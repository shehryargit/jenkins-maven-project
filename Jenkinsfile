pipeline {
    agent {label 'server1'}
    environment {
        FIRST_NAME = 'Shehryar'
    }
    parameters {
        choice choices: ['dev'], name : select_environment 
    }
    tools {maven 'maven'}
    stages {
        stage('build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage('test') {
            parallel {
                agent {label 'server2'}
                stage ('Test A') {
                    steps {
                        echo 'Running test A'
                        sh 'mvn test'
                    }
                }
                agent {label 'server3'}
                stage ('Test B'){
                    steps {
                        echo 'Running test B'
                        sh 'mvn test'
                    }
                }
            }
            }
    post {
        success {
            dir('webapp/target/') {
                stash name: 'maven-build', includes: '*.war'
            }
        }
    }
    stage('deploy') {
        when {expression {params.select_environment == 'dev'}
        beforeAgent true
        agent {label 'server1'}
        steps {
            dir('var/www/html') {
                unstash 'maven-build'
            }
            sh """
            cd /var/www/html
            jar -xvf  webapp.jar
            """
        }
        }
    }

        }
}