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
   stage('ContinuousBuild')
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
   stage('ContinuousDeployment')
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
}

