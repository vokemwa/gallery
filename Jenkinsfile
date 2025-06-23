pipeline {
     agent any
   
     tools {
        nodejs 'NodeJS-24'
    }
    
   stages{
       stage('Clone Repo') {
            steps {
                git branch: 'master', url: 'https://github.com/vokemwa/gallery.git'
            }
        }
       stage('npm install'){
           steps{
               sh 'npm install'  //install npm node1
           }
       }
       
       stage('Run Application Tests') {
            steps {
                sh 'npm test'
            }
       }
       
   
   }
   
    post {
        success {
            echo "✅ Build succeeded."
        }
    failure {
        emailext (
            to: 'vinorex23@gmail.com',
            subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: """The build failed.
Check the details here:
${env.BUILD_URL}
"""
        )
    }
}
       
 }
