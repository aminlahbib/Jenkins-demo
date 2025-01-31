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
                       sh 'docker-compose -f docker-compose.yml build backend'
                   }
               }
           }
           stage ('Build Frontend') {
               steps {
                   script {
                       sh 'docker-compose -f docker-compose.yml build frontend'
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
           stage ('Test') {
               steps {
                   script {
                       // Add your testing commands here
                       echo 'Running tests...'
                   }
               }
           }
       }
   }