node('') {
	stage ('checkout code'){
		checkout scm
	}
	
	stage ('Build'){
		sh "mvn clean install -Dmaven.test.skip=true"
	}

	stage ('Test Cases Execution'){
		sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
	}

	stage ('Sonar Analysis'){
		//sh 'mvn sonar:sonar -Dsonar.host.url=http://35.153.67.119:9000 -Dsonar.login=77467cfd2653653ad3b35463fbfdb09285f08be5'
	}

	stage ('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}
	
	stage ('Deployment'){
		//ansiblePlaybook colorized: true, disableHostKeyChecking: true, playbook: 'deploy.yml'
		deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '',url: 'http://34.204.12.206:8080/')], contextPath: 'counterwebapp', war:'target/*.war'
	}
	
	stage ('Notification'){
		emailext (
		      subject: "Job Completed",
		      body: "Jenkins Pipeline Job for Maven Build got completed !!!",
		      to: "swatee.swatee123@gmail.com"
		    )
	}
}
