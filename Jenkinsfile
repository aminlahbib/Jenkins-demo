   pipeline {
       agent any
       stages {
           stage('Clone Repository') {
               steps {
                   git 'git@github.com:aminlahbib/Jenkins-demo.git'
               }
           }
           stage('Build Docker Images') {
               steps {
                   script {
                       sh 'docker build -t my-db ./db'
                       sh 'docker build -t my-backend ./backend'
                       sh 'docker build -t my-frontend ./frontend'
                   }
               }
           }
           stage('Run Docker Containers') {
               steps {
                   script {
                       // Run database
                       sh 'docker run -d --name my-db -e MYSQL_DATABASE=swtp -p 3306:3306 mysql:latest'
                       // Run backend
                       sh 'docker run -d --name my-backend --link my-db -p 8080:8080 my-backend'
                       // Run frontend
                       sh 'docker run -d --name my-frontend -p 8081:8081 my-frontend'
                   }
               }
           }
       }
       post {
           always {
               // Clean up
               sh 'docker stop my-frontend my-backend my-db'
               sh 'docker rm my-frontend my-backend my-db'
           }
       }
   }