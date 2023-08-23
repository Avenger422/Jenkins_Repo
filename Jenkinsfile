pipeline {
    agent any
    
    stages {
        stage('Get-Code') {
            steps {
                checkout([
            $class: 'GitSCM',
            branches: [[name: 'main']], // Specify the branch you want to checkout
            userRemoteConfigs: [[url: 'https://github.com/Avenger422/Jenkins_Repo.git']],
            credentialsId: 'f2840e72-0a66-4c57-91b1-529ea15441e0' // Specify your credentials ID here
        ])
                }     
            }
            
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deliver') {
            steps {
                sshagent(credentials: ['5ef95c33-9d5f-4c4a-a421-de8ec24998b6']) {
                    sh 'scp -o StrictHostKeyChecking=no target/maven-project-1.0-SNAPSHOT.war tomcatuser@172.174.43.139:/home/tomcatuser/apache-tomcat-9.0.78/webapps'
                }
            }
        }
    }
}
