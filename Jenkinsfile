node {
    stage('SCM') {
        git 'https://github.com/abhishek101329/spring-petclinic.git'
		}
		
	stage('Build & Package') {
		bat 'mvn package'
	
	}	
	
	stage('SonarQube analysis') {
		withSonarQubeEnv('') { // Will pick the global server connection you have configured in Jenkins global configuration
			bat './gradlew sonarqube'
			}
		}
	stage("Quality Gate"){
		timeout(time: 1, unit: 'HOURS') 
		def qg = waitForQualityGate()
			if (qg.status != 'OK') {
			error "Pipeline aborted due to quality gate failure: ${qg.status}"
    }
  }
}	

	
	

	