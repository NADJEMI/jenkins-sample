// Powered by Infostretch 

timestamps {

node () {

	stage ('Jenkins DEV Token_Sample_APP_IC - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '1a4ee13a-3792-4db1-8afd-d2c1b71aa1f5', url: 'https://github.com/NADJEMI/jenkins-sample.git']]]) 
	}
	stage ('Jenkins DEV Token_Sample_APP_IC - Build') {
 			// Maven build step
	withMaven(maven: 'MAVEN') { 
 			if(isUnix()) {
 				sh "mvn clean package " 
			} else { 
 				bat "mvn clean package " 
			} 
 		} 
	}

	stage('Quality check') {
		withSonarQubeEnv('Sonar') {
			bat "mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar
			-Dsonar.projectKey=jenkins-demo"
		}
	}
	stage ('Jenkins DEV Token_Sample_APP_IC - Post build actions') {
/*
Please note this is a direct conversion of post-build actions. 
It may not necessarily work/behave in the same way as post-build actions work.
A logic review is suggested.
*/
		// Mailer notification
		step([$class: 'Mailer', notifyEveryUnstableBuild: false, recipients: 'nadjemi@gmail.com', sendToIndividuals: false])
 
	}
}
}
