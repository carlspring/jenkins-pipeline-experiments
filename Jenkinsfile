pipeline {
    agent { label 'opensuse-sonar-docker' }
    stages {
        stage('Build') {
            steps {
                checkout scm
                try {
                    sh 'mvn clean install'
                }
                finally {
                    junit '**/target/*.xml'
                }
            }
        }
        stage('Build on other OS\'s') {
            steps {
                parallel(
                    "Build on Windows": {
                        node('windows') {
                            checkout scm
                            bat 'mvn clean install'
                        }
                        finally {
                            junit '**/target/*.xml'
                        }
                    }
                )
            }
        }
        stage('Deploy to stage') {
            steps {
                echo 'Deploying to stage.'
            }
        }
        stage('Integration tests') {
            steps {
                echo 'Running integration tests.'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Running deploying to production.'
            }
        }
    }
}
