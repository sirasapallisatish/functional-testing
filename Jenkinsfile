node('built-in') 
{
   stage('ContinuousDownload')
   {
       try
       {
          git 'https://github.com/sirasapallisatish/maven1.git'
       }
       catch(Exception e1)
       {
           mail bcc: '', body: 'Jenkins is unable to download from the remote github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.admin@gmail.com'
            exit(1)
       }
   }
   stage('ContinuousBuild_master')
   {
       try
       {
           sh 'mvn package'
       }
       catch(Exception e2)
       {
           mail bcc: '', body: 'Jenkins is unable to create an artifact from the downloaded code', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'dev.team@gmail.com'
           exit(1)
       }
   }
   stage('ContinuousDeployment_master')
   {
       try
       {
         deploy adapters: [tomcat9(credentialsId: '44d1f586-db66-40ca-bcb8-e54891648131', path: '', url: 'http://172.31.3.197:8080')], contextPath: 'testapp', war: '**/*.war'
       }
       catch(Exception e3)
       {
            mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the QAservers', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middleware.team@gmail.com'
            exit(1)
       }
   }
   stage('ContinuousTesting_master')
   {
       try
       {
         git 'https://github.com/sirasapallisatish/functional-testing.git'
       }
       catch(Exception e4)
       {
           mail bcc: '', body: 'Selenium scripts are showing a failure status', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'qa.team@gmail.com'
           exit(1)
       }
   }
   stage('ContinuousDelivery_master')
   {
       try
       {
          input message: 'approval from last stage', submitter: 'karthik'
         deploy adapters: [tomcat9(credentialsId: '44d1f586-db66-40ca-bcb8-e54891648131', path: '', url: 'http://172.31.1.101:8080')], contextPath: 'prodapp', war: '**/*.war'
       }
       catch(Exception e5)
       {
           mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the prodservers', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'delivery.team@gmail.com'   
       }
   }
   
}

:
