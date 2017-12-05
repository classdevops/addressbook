node {'master'
   def mvnHome
   def version 
   stage('Checkout') {
      git 'https://github.com/classdevops/addressbook.git'
      mvnHome = tool 'LOCAL_MAVEN'
	  version = '2.3.5' 
	   // THIS IS ON DEVELOP BRANCH.
   }
   stage('Build') {
        withMaven(
        maven: 'LOCAL_MAVEN', // Maven installation declared in the Jenkins "Global Tool Configuration"
        mavenSettingsConfig: 'settings.xml', // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
        mavenLocalRepo: 'd:/repos')
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore test -Pfunctional-test -DSkipUTs=true -DskipTests=true"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore test -Pfunctional-test -DSkipUTs=true -DskipTests=true/)
      //git 'https://github.com/sachingupta771/addressbook.git'
      //mvnHome = tool 'LOCAL_MAVEN'
	//  version = '3.3.9' 
   }
   }
   stage('Perform-UnitTest') {
        withMaven(
        maven: 'LOCAL_MAVEN', // Maven installation declared in the Jenkins "Global Tool Configuration"
        mavenSettingsConfig: 'settings.xml', // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
        mavenLocalRepo: '/opt/maven') 
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn'  clean test"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean test/)

      }
    } // withMaven will discover the generated Maven artifacts, JUnit reports and FindBugs reports
    

   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
     stage('DeployToServer') {
	 } 
   stage('PublishResults') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }

   stage('notify') { 
   }
}
