pipeline {
    agent any 
    tools {
        maven 'Maven 3.8.1'
        jdk 'jdk8'
    }
    stages {
        stage ('Build') {
            steps {    
                sh ' mvn clean install -DskipTests'
            }
        }
        /*stage ('Test') {
            steps {    
                sh ' mvn test'
            }
        }*/        
        stage ('Imagem docker') {
            steps {
                sh 'docker build . -t vonex/api_eureka:${BUILD_NUMBER}'
            }
        }
        stage ('Run docker') {
            steps {
                sh ' docker stop integra-eureka' 
                sh ' docker rm integra-eureka'                
                sh ' docker container run -d --name integra-eureka -p 8761:8761 vonex/api_eureka:${BUILD_NUMBER}'
            }
        }        
    }
}


