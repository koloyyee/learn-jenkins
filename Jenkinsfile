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
    // agent {
    //     node {
    //         label 'docker-agent-spring'
    //         }
    //   }
    //   triggers {
    //     pollSCM '* * * * *'
    //   }
    agent any
    // environment {
    //     DOCKER_COMPOSE_FILE = 'docker-compose.yml'
    // }
    stages {
        // stage('Clone Repository') {
        //     steps {
        //         // Clone the GitHub repository
        //         git branch: 'main', url: 'git@github.com:yourusername/yourrepo.git'
        //     }
        // }
        stage('Build and Deploy') {
            steps {
                // Build and deploy the Docker container
                script {
                    // sh 'docker-compose down'
                    // sh 'docker-compose up --build --detach'
                    echo "hello"
                }
            }
        }
    }
    // post {
    //     always {
    //         // Clean up resources
    //         sh 'docker-compose down'
    //     }
    // }
}
