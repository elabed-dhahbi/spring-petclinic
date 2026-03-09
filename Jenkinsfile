pipeline {
   agent { label 'JDK17' }

   environment {
      MVN = '/opt/maven/current'
   }

   options {
      timeout(time: 1, unit: 'HOURS')
      retry(3)
   }

   triggers {
      cron('H */4 * * *')
   }

   stages {

      stage('Git Clone') {
         steps {
            git url: 'https://github.com/elabed-dhahbi/spring-petclinic.git', branch: 'main'
         }
      }

      stage('Build the code') {
         steps {
            sh "$MVN/bin/mvn clean package"
         }
      }

      stage('Reporting and Archiving') {
         steps {
            junit 'target/surefire-reports/*.xml'
         }
      }

   }

   post {
      success {
         echo "Success"
      }

      unsuccessful {
         echo "failed"
      }
   }
}
