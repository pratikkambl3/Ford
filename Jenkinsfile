pipeline{
     agent any
     triggers {
  pollSCM '* * * * *'
}
     parameters {
  choice choices: ['DEV', 'QA', 'UAT'], name: 'ENV'
                 }

     stages{
            stage("Checkout"){
                   steps{
                        checkout scm
                           }
                             }
             stage("Build"){
                  steps{
                 sh '/home/vboxuser/Documents/DevopsTools/apache-maven-3.9.6/bin/mvn install'

                        }
                            }
             stage("Failed-Noti"){
                       steps{
                                                 slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#ford', color: 'danger', failOnError: true, message: 'build is failed', teamDomain: 'DEVOPS', tokenCredentialId: 'Ford1', username: 'SIRI'
                             }
                                 }
             
             stage("Deployment"{
                     steps{
                 
                        sh '''if [ $ENV = "DEV" ];then
cp target/Ford.war /home/vboxuser/Documents/DevopsTools/apache-tomcat-9.0.88/webapps
echo "Deployed to DEV SERVER"
elif [ $ENV = "QA" ];then
cp target/Ford.war /home/vboxuser/Documents/DevopsTools/apache-tomcat-9.0.88/webapps
echo "Deployed to QA SERVER"
elif [ $ENV = "UAT" ];then
cp target/Ford.war /home/vboxuser/Documents/DevopsTools/apache-tomcat-9.0.88/webapps
echo "Deployed to UAT SERVER"
fi'''
                            }
                                 }
                      stage("notification"){
                               steps{
                             slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#ford', color: 'good', failOnError: false, message: 'build is successful', teamDomain: 'DEVOPS', tokenCredentialId: 'Ford1', username: 'SIRI'                                                                         
   }
                                          }
       


           }
}
