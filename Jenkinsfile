node{
 stage('Source'){
    git branch: 'test_branch', credentialsId: 'latest-github-cred', url: 'https://github.com/NagireddyGuduru/client-demo-project.git'
 }
  def mvnHome = tool 'Maven HOme'
 stage('Build'){
      bat "${mvnHome}/bin/mvn clean install" 
  }
  stage('CodeQualityCheck'){
      bat "${mvnHome}/bin/mvn clean sonar:sonar" 
  }
  stage('UploadArtifacts'){
      bat "${mvnHome}/bin/mvn clean deploy" 
  }
  stage('DeployApplication'){
      echo "Deploying the application using chef"
  }
  stage('Run Selenium Test'){
      echo "Running Selenium Test"
  }
  stage('Performane Tests'){
                bat '''D:
				cd D:\\Jmeeter\\apache-jmeter-3.1\\bin
	            jmeter -n -t D:\\Jmeeter\\apache-jmeter-3.1\\extras\\Test.jmx -l D:\\Jmeeter\\demo-report.jtl'''
              
    			performanceReport compareBuildPrevious: false, configType: 'ART', errorFailedThreshold: 0, errorUnstableResponseTimeThreshold: '', errorUnstableThreshold: 0, failBuildIfNoResultFile: false, modeOfThreshold: false, modePerformancePerTestCase: true, modeThroughput: false, nthBuildNumber: 0, parsers: [[$class: 'JMeterParser', glob: 'D:\\Jmeeter\\demo-report.jtl']], relativeFailedThresholdNegative: 0, relativeFailedThresholdPositive: 0, relativeUnstableThresholdNegative: 0, relativeUnstableThresholdPositive: 0
            }
   }
 