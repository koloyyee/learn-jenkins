// pipeline {
//     agent { 
//         node {
//             label 'docker-agent-spring'
//             }
//       }
//       triggers {
//         pollSCM '*/1 * * * *'
//       }
//     stages {
//         stage('Build') {
//             steps {
//                 echo "Building.."
//                 sh '''
//                 cd j
//                 docker pull maven:3.9-eclipse-temurin-21-alpine
//                 mvn clean package -DskipTests
//                 docker compose -f docker-compose.yml --build
//                 '''
//             }
//         }
//         stage('Test') {
//             steps {
//                 echo "Testing.."
//                 sh '''
//                 cd j
//                 mvn test
//                 '''
//             }
//         }
//         stage('Deliver') {
//             steps {
//                 echo 'Deliver....'
//                 sh '''
//                 cd j
//                 docker compose -f docker-compose.yml --build --detach
//                 '''
//             }
//         }
//     }
// }

pipeline {
  agent any
  stages {
    stage("verify tooling") {
      steps {
        sh '''
          docker compose version 
          curl --version
          jq --version
        '''
      }
    }
    stage('Prune Docker data') {
      steps {
        sh 'docker system prune -a --volumes -f'
      }
    }
    stage('Start container') {
      steps {
        sh 'docker compose up -d --no-color --wait'
        sh 'docker compose ps'
      }
    }
    stage('Run tests against the container') {
      steps {
        sh 'curl http://localhost:3000/param?query=demo | jq'
      }
    }
  }
  post {
    always {
      sh 'docker compose down --remove-orphans -v'
      sh 'docker compose ps'
    }
  }
}