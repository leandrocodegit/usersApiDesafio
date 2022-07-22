pipeline { 
    agent any
    stages{
         stage('Permission') {  
            steps{
                sh 'chmod 777 /var/jenkins_home/workspace/Delivery-build@tmp'
            }
        }
        stage('Build') { 
            steps{
                sh './gradlew build'
            } 
        }
       
    }
}
