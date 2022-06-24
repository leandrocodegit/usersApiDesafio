pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                gradlew('clean', 'classes')
            }
        }
        stage('Unit Tests') {
            steps {
                gradlew('test')
            }
            post {
                always {
                    junit '**/build/test-results/test/TEST-*.xml'
                }
            }
        }
        stage('Build & Push docker image') {
            steps {
               withDockerRegistry(credentialsId: '67112d83-1551-4f97-b550-ee5e6e42f437', url: 'https://index.docker.io/v1/') {
                    sh 'docker push eosh/api-user-gft:tagname'
                }
            }
        }
    }
    post {
        failure {
            mail to: 'eosh@gft.com', subject: 'Build failed', body: 'Please fix!'
        }
    }
}

def gradlew(String... args) {
    sh "./gradlew ${args.join(' ')} -s"
}
