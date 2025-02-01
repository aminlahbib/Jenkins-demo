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
                       // Change to the backend directory and build the backend JAR file
                       dir('backend') {
                           sh '''
                           ls
                           mvn clean package -DskipTests
                           '''
                       }
                       // Change back to the main directory to build the Docker image for the backend
                       dir('.') {
                           sh 'docker-compose -f docker-compose.yml build backend'
                       }
                   }
               }
           }
           stage ('Build Frontend') {
               steps {
                   script {
                       // Build the Docker image for the frontend
                       sh 'docker-compose -f docker-compose.yml build frontend'
                   }
               }
           }
           stage ('Run Tests') {
               steps {
                   script {
                       // Run backend tests
                       sh 'mvn test'
                       // Add frontend test commands if applicable
                       echo 'Running frontend tests...'
                   }
               }
           }
           stage ('Deploy') {
               steps {
                   script {
                       // Deploy the application
                       sh 'docker-compose -f docker-compose.yml up -d'
                   }
               }
           }
       }
   }