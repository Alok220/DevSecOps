pipeline {
  agent any
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
       sh '''
       echo "PATH = $(PATH)"
       echo "M2_HOME = $(M2_HOME)"
          '''
      }
    }
    
    stage ('Check-Git-Secrets') {
      steps {
        sh ' rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/Alok220/DevSecOps.git > trufflehog'
        sh 'cat trufflehog'
    }
  }
    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
    }
    }
   
     stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['ubuntu']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.232.48.171:/home/ubuntu/prod/apache-tomcat-9.0.65/webapps/webapp.war'
              }      
           }       
    }
    
  }
}
