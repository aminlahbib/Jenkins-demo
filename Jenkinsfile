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
                       // Build the backend JAR file
                       sh 'mvn clean package -DskipTests'
                       // Build the Docker image for the backend
                       sh 'docker-compose -f docker-compose.yml build backend'
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