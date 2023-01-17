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
                deploy adapters: [tomcat10(credentialsId: 'ubuntuask', path: '', url: 'http://65.2.175.124:8080')], contextPath: '/app', war: '**/*.war'
              
            }
            
        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat10(credentialsId: 'ubuntupass', path: '', url: 'http://13.235.50.240:8080')], contextPath: '/app', war: '**/*.war'

            }
        }
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
