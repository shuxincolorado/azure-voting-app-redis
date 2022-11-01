pipeline {
   agent any

   stages {
      
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
            powershell 'Write-Output "Hello from powershell"'
            powershell 'docker imapowershellges -a'
            powershell """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """
         }
      }
      
   }
}
