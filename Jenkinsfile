pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                        userRemoteConfigs: [[url: 'https://github.com/aminlahbib/Jenkins-demo.git']]
                    ])
                }
            }
        }
        stage ('Verify Git Directory') {
            steps {
                script {
                    sh 'pwd'
                    sh 'ls -la'
                }
            }
        }
        stage ('Build') {
            steps {
                script {
                    dir('Jenkins-demo-app') {  // Adjust to your repo folder name
                        sh 'git rev-parse --is-inside-work-tree'
                        sh 'mvn clean package -DskipTests'
                    }
                }
            }
        }
    }
}
