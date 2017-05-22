node{
 stage('Source'){
	 echo "In This Stage, Getting the source code from GitHub"
    checkout scm
 }
  def mvnHome = tool 'MAVEN_HOME'
 stage('Build'){
	 echo "In this Stage, Doing compile and package"
      bat "${mvnHome}/bin/mvn clean install" 
  }
  stage('CodeQualityCheck'){
	  echo "In This Stage, Doing static code analysis and Code coverage"
      bat "${mvnHome}/bin/mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test sonar:sonar" 
  }
  stage('UploadArtifacts'){
	  echo "In This Stage, Uploading Compiled Code Binaries into Nexus"
      bat "${mvnHome}/bin/mvn clean deploy" 
  }
  stage('DeployApplication'){
      echo "In This Stage, Triggering Deploying the application using chef"
       bat "copy target\\myweb.war C:\\apache-tomcat-7.0.72\\webapps\\"
	  
  }
 stage('Run Selenium Tests'){
	 echo "In This Stage, Triggering a job to Run Selenium Tests"
	 build job: 'DEVOPS_DEMO_PROJECT/AUTOMATE_DEPLOYEMENT_PROCESS/RunSeleniumTests'
  //  dir ("D:\\PROJECT_INFO\\DEVOPS\\selenium_project_bat_file") { 
  //      bat 'Selenium.bat' 
    // } 
  }
  stage('Performane Tests'){
	  echo "In This Stage, Triggering a job to Run Performance Tests"
	  build job: 'DEVOPS_DEMO_PROJECT/AUTOMATE_DEPLOYEMENT_PROCESS/RunPerformanceTest'
      //          bat '''D:
	//			cd D:\\Jmeeter\\apache-jmeter-3.1\\bin
	  //          jmeter -n -t D:\\Jmeeter\\apache-jmeter-3.1\\extras\\Test.jmx -l D:\\Jmeeter\\demo-report.jtl'''
            //  
    		//	performanceReport compareBuildPrevious: false, configType: 'ART', errorFailedThreshold: 0, errorUnstableResponseTimeThreshold: '', errorUnstableThreshold: 0, failBuildIfNoResultFile: false, modeOfThreshold: false, modePerformancePerTestCase: true, modeThroughput: false, nthBuildNumber: 0, parsers: [[$class: 'JMeterParser', glob: 'D:\\Jmeeter\\demo-report.jtl']], relativeFailedThresholdNegative: 0, relativeFailedThresholdPositive: 0, relativeUnstableThresholdNegative: 0, relativeUnstableThresholdPositive: 0
            }
   }
