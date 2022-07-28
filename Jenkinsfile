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
    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
    }
    }
   
     stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp ubuntu@15.206.92.63:/var/lib/jenkins/workspace/webapp-build-cicd-job/target/WebApp.war ubuntu@13.232.48.171:/prod/apache-tomcat-9.0.65/webapps/webapp.war'
              }      
           }       
    }
    
  }
}
