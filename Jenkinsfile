node
{
	try{
          stage('Project Name')
          {
            echo 'Complete CICD Pipeline'
          }

          stage('Checkout Code')
         {
           git 'https://github.com/AshutoshKumar99/MavenProjectRepository'
         }

         stage('Build Code')
         {

           sh 'mvn clean install -Dmaven.test.failure.ignore=true'
         }

         stage ('Archieve_it')
        {
          archive "target/**/*"
       }
	    stage ('JUnit Report')
        {
         junit 'target/surefire-reports/*.xml' 
       }
        stage('Slage notification')
        {
         slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkinspipelinedemo', color: 'good', message: 'Welcome to jenkins, slack !', teamDomain: 'Ashutosh DevOps', tokenCredentialId: 'slackdemo'
        }
      stage('Deploy to Tomcat')
      {  
	  sshagent(['apachetomcat']) 
       {
        sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.233.162.162:/var/lib/tomcat8/webapps/'
       }  
   }  } catch (err) {
	    emailext body: "Cought Error: ${err}", subject: 'Build failed', to: 'ashutosh.kumar@pb.com'
	  }
}
