//dev branch pipeline
pipeline
{
	
   agent any
   tools
   {
      maven "maven-3.9.6"
   }
   stages
   {
           stage('git checkout')
           {
              steps
              {
                 git branch: 'dev', url: 'https://github.com/Geetha0307/maven-webapplication-project-kkfunda.git'
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
           stage('SQ REPORT')
           {
             steps
             {
                sh "mvn sonar:sonar"
             }
           }
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

      curl -u geetha:password \
--upload-file /var/lib/jenkins/workspace/jio-Declarative-PL-dev/target/maven-web-application.war \
"http://65.1.94.57:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
              }
           }
	      stage('bsnl-qa')
       {
           steps
           {
               build job:'bsnl-QA' //downstream job
           }
       }

   }  //stages ending


} //pipeline ending
