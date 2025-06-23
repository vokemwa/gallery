pipeline {
     agent any
   
     tools {
        nodejs 'NodeJS-24'
    }

    environment {
        SLACK_CHANNEL = '#Vincent_IP1'
        SLACK_CREDENTIAL_ID = 'test'
        SITE_URL = 'https://ip1-project.onrender.com' // Replace with actual Render URL
    }
    
   stages{
       stage('Clone Repo') {
            steps {
                git branch: 'master', url: 'https://github.com/vokemwa/gallery.git'
            }
        }
       stage('npm install'){
           steps{
               sh 'npm install'  //install npm node11
           }
       }

       stage('Build') {
            steps {
                sh 'npm run build
            }
        }
       
       stage('Run Application Tests') {
            steps {
                sh 'npm test'
            }
       }

       stage('Deploy') {
            steps {
                echo 'deploy...'
                
                echo 'App URL: https://ip1-project.onrender.com'
            }
        }

       stage('Notification to Slack') {
            steps {
                slackSend (
                    channel: "${SLACK_CHANNEL}",
                    color: 'good',
                    message: "✅ Build #${env.BUILD_ID} deployed! Visit: ${SITE_URL}",
                    tokenCredentialId: "${SLACK_CREDENTIAL_ID}"
                )
            }
        }     
       
   
   }
   
    post {
        success {
            echo "✅ Build succeeded."
        }
    failure {
        slackSend (
                channel: "${SLACK_CHANNEL}",
                color: 'danger',
                message: "❌ Build #${env.BUILD_ID} failed!",
                tokenCredentialId: "${SLACK_CREDENTIAL_ID}"
            )
    }
}
       
 }
