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
            powershell 'docker images -a'
            powershell """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """
         }
      }

      stage('Start test app') {
         steps {
            powershell """
               docker compose up -d
               ./scripts/test_continer.ps1
            """
         }

         post{
            success{
               echo "App started successfully :)"
            }

            failure{
               echo "App failed to start"
            }
         }
      }
      
      stage('Run Tests') {
         steps {
            powershell """
               pytest ./tests/test_sample.py
            """
         }
      }

      stage('Stop Tests') {
         steps {
            powershell """
               docker-compose down
            """
         }
      }
   }
}
