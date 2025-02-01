pipeline {
    agent any
    stages {
        stage ('hello') {
            steps {
                echo 'hello world'
            }
        }
        stage ('Build Backend') {
            steps {
                script {
                    dir('backend') {
                        sh 'ls'
                        sh 'mvn clean package -DskipTests'
                    }
                    dir('.') {
                        sh 'docker-compose -f docker-compose.yml build backend'

                    }
                }
            }
        }
        stage ('Build Frontend') {
            steps {
                script {
                    dir('frontend') {
                        sh 'docker-compose -f ../docker-compose.yml build frontend'
                    }
                }
            }
        }
        stage ('Run Tests') {
            steps {
                script {
                    dir('backend') {
                        sh 'mvn test'
                    }
                    echo 'Running frontend tests...'
                    // Add frontend test commands if applicable
                }
            }
        }
        stage ('Deploy') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose.yml up -d'
                }
            }
        }
    }
}
