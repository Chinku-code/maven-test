pipeline {
 agent none
 stages{
  stage("build and SonarQube Analysis")
  {
   agent any
    steps {
	 withSonarQubeEnv('test')
	 {
	  sh "mvn clean package sonar:sonar -Dsonar.projectKey=mavenproject -Dsonar.projectName='mavenproject'"
	 }
	}
  }
 }
}
