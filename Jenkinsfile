pipeline {
   agent { label 'JDK17' }
   environment {
      MVN = '/opt/maven/current'
   }
   options {
      timeout(time:1,unit: 'HOURS')
      retry(3)
   }
   triggers {
     cron('H */4 * * * 1-54' )
   }
   stages {
      stage('Git Clone' ) {
         steps {
             git url: 'https://github.com/elabed-dhahbi/spring-petclinic.git', branch: 'main'
         }
      }
      stage('Build the code') {
        steps {
           sh script: '"$MVN clean package"'
        }
      }
      stage('Reporting and Archiving') {
         steps {
            junit testResults: 'target/surefire-reports/*.xml'
         }
      }
      post {
      success {
          //send the sucess email
          echo "Success"
        }
        unsuccessful {
        //send the failure email
        echo "failed"
        }
      }
   }
}
