pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
         stage ('Deploy to Staging'){
            steps{
                timeout(time:2, unit:'DAYS'){
                    input message:'Approve Deployment?'
                }

                build job: 'Deploy-to-Staging'
            }
            post {
                success {
                    echo 'Code deployed to Staging.'
                }

                failure {
                    echo ' Deployment failed on Staging'
        
                }
   
            }
         }
         stage ('Continuous Inspection'){
          steps{
                build job: 'Continuous Inspection'
            }
            post {
                success {
                    echo 'Inspection....'
                }  
            }
        }
    }
}
        
       
