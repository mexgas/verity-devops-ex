pipeline {
    agent any
    stages {
		
      stage('Clean'){
        steps{
          sh 'mvn clean'
        }
      }
      
      stage('PMD'){
        steps{
          sh 'mvn site'
        }
      }
      stage('Compile'){
        steps{
          sh 'mvn compile'
        }
      }
      stage('Code Analysis') {
        steps {
          script {
              scannerHome = tool 'sonar-scanner'
            }
            withSonarQubeEnv('sonar')
            {
            sh "${scannerHome}/bin/sonar-scanner"
            }
        }
      }

      stage('Unit Test'){
        steps{
          sh 'mvn test'
        }      
        post{
          always{
            junit 'target/surefire-reports/*.xml'
          }
        }
      }
		// ******ALL CODE TO BE ADDED BELOW THIS COMMENT******
		
	
	
		// ******ALL CODE TO BE ADDED ABOVE THIS COMMENT******
    }
}