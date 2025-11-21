pipeline {
  agent any
  tools { 
        maven 'maven_3_5_2'  
    }
   stages{
    stage('Run Sonar Analysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectkey=demo-sast-1 -Dsonar.organization=demo-sast-1 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=e4e706095b5701b7b0fbec230536b78f6e467cad'
		//sh 'mvn clean compile sonar:sonar -Dsonar.projectKey=franksast -Dsonar.organization=franksast -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=ce3caf6f60b599b72a6ced8a5fc17e060b1d87ee'
			}
        }
    // stage('Run SCA Analysis using Snyk') {
    //         steps {		
		// 	withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
		// 	    sh 'mvn snyk:test -fn'
		// 		}
		// 	}
    // }	


  }
}
