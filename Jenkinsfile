pipeline
{
	
   agent any
   tools
   {
      maven "maven-3.9.8"
   }
   stages
   {
           stage('git checkout')
           {
              steps
              {
                 notifyBuild('STARTED') 
                 git branch: 'dev', url: 'https://github.com/kkdevopsb7/maven-webapplication-project-kkfunda.git'
              }
           }
           stage('compile')
           {
              steps
              {
                 sh "mvn compile"
              }
           }
           stage('Build')
           {
             steps
             {
               sh "mvn clean package"
             }
           }
         /*  stage('SQ REPORT')
           {
             steps
             {
                sh "mvn sonar:sonar"
             }
           }   */
           stage('Deploy to nexus')
           {
              steps
              {
                sh "mvn clean deploy"
              }
           }
           stage('Deploy to tomcat')
           {
              steps
              {
                 sh """

      curl -u kk:password \
--upload-file /var/lib/jenkins/workspace/jio-Declarative-PL-dev/target/maven-web-application.war \
"http://13.201.83.168:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
              }
           }

   }  //stages ending

post {
  success {

    script
    {
     notifyBuild(currentBuild.result)
    }
    
  }
  failure {

  script
  {
    notifyBuild(currentBuild.result)

  }
   
  }
}



} //pipeline ending
