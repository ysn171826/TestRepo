node{
 stage('Source'){
    checkout scm
 }
  def mvnHome = tool 'Maven HOme'
 stage('Build'){
      bat "${mvnHome}/bin/mvn clean install" 
  }
 stage('DeployApplication'){
      bat 'copy target\\myweb.war C:\\apache-tomcat-7.0.72\\webapps\\'
     }
 }
 
