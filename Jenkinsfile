pipeline {
    agent any
    
    stages {
        stage ('Test & Build Artifact') {
            agent {
                docker {
                    image 'openjdk:17'
                    args '-v "$PWD":/app'
                    reuseNode true
                }
            }
            steps {
                sh './gradlew clean build'
            }
        }
        stage ('Build & Push docker image') {
            steps {
                withDockerRegistry(credentialsId: '67112d83-1551-4f97-b550-ee5e6e42f437', url: 'https://index.docker.io/v1/') {
                    sh 'docker push eosh/api-user-gft:tagname'
                }
            }
        }
    }
}