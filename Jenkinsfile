pipeline {
  agent any
  tools { 
    maven 'Java_Maven'  
    }
  
  stages {
      stage('Run Sonar Analysis') {
        environment {
          SONAR_TOKEN = credentials('SONARQUBE_TOKEN')
                }
        steps {
		      sh """
          mvn clean verify sonar:sonar \
          -Dsonar.projectKey=demo-sast-1 \
          -Dsonar.organization=demo-sast-1 \
          -Dsonar.host.url=https://sonarcloud.io \
          -Dsonar.login=$SONAR_TOKEN
        """
			          }
            }
      stage('Run SCA Analysis using Snyk') {
        steps {		
          withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
            sh """
            snyk auth ${SNYK_TOKEN}
            snyk test --all-projects --severity-threshold=medium
            snyk monitor --all-projects
          // 'mvn snyk:test -fn'
            """
          }
        }
      }

      post {
        always {
            junit '**/target/surefire-reports/*.xml'          // Test results
            archiveArtifacts '**/target/site/jacoco/*.xml'    // Coverage reports
          }
        failure {
            echo 'Build failed. Check SonarQube and Snyk reports.'
        }
      }
  }
}