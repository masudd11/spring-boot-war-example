pipeline {
    agent any
     tools {
        maven 'Maven' 
        }
    stages {
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
//                 slackSend channel: 'youtubejenkins', message: 'Job Started'
                
            }
            
        }
        stage("Build"){
            steps{
                sh "mvn package"
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
//               deploy adapters: [tomcat9(credentialsId: 'bus', path: '', url: 'http://13.235.50.240:8080')], contextPath: '/app', war: '**/*.war'
                sshagent(['sshid']) {
                // some block
                    sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/fresh/target/hello-world-0.0.1-SNAPSHOT.war ubuntu@3.108.66.159:/opt/tomcat10/webapps/'
                }
              
            }
            
        }
//         stage("Deploy on Prod"){
//              input {
//                 message "Should we continue?"
//                 ok "Yes we Should"
//             }
            
//             steps{
//                 // deploy on container -> plugin
//                 deploy adapters: [tomcat9(credentialsId: 'ubuntupass', path: '', url: 'http://13.235.50.240:8080')], contextPath: '/app', war: '**/*.war'

//             }
//         }
    }
    post{
        always{
            echo "========always========"
        }
//         success{
//             echo "========pipeline executed successfully ========"
//              slackSend channel: 'youtubejenkins', message: 'Success'
//         }
//         failure{
//             echo "========pipeline execution failed========"
//              slackSend channel: 'youtubejenkins', message: 'Job Failed'
//         }
    }
}
