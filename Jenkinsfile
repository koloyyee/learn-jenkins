pipeline {
    agent { 
        node {
            label 'docker-agent-spring'
            }
      }
      triggers {
        pollSCM '*/1 * * * *'
      }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd j
                docker pull maven:3.9-eclipse-temurin-21-alpine
                mvn clean package -DskipTests
                docker compose -f docker-compose.yml --build
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                cd j
                mvn test
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                cd j
                docker compose -f docker-compose.yml --build --detach
                '''
            }
        }
    }
}
