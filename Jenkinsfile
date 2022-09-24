pipeline {
    agent any
    stages {
            
        // ******ALL CODE TO BE ADDED BELOW THIS COMMENT******
            
        //Code starts for stage Clean
        stage('Clean') {
            steps {
                sh 'mvn clean'
            }
        }
        //Code ends for stage Clean
        
        
        //Code starts for stage PMD
        stage('PMD') {
            steps {
                sh 'mvn site'
            }
        }
        //Code ends for stage PMD
        
        
        //Code starts for stage Compile
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        //Code ends for stage Compile
        
        
        //Code starts for stage Code Analysis
        stage('Code Analysis') {
            steps {
             script {
          scannerHome = tool 'sonar-scanner'
        }
                withSonarQubeEnv('My SonarQube Server')
                {
                sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        //Code ends for stage Code Analysis
        
        
        //Code starts for stage Unit Test
        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }    
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        //Code ends for stage Unit Test
        
        
        //Code starts for stage Code Coverage
        stage('Code Coverage') {
            steps {
              // generate
              step ([
                $class: 'JacocoPublisher'
              ])
            }
        }
        //Code ends for stage BDD Test    
        stage('Install') {
            steps {
                sh 'mvn install -DskipTests'
            }
        }
        //Code ends for stage Install
        
        
        //Code starts for stage Launch Tomcat Server
        stage('Launch Tomcat Server') {
            steps {
                sh '/tmp/apache-tomcat-9.0.20/bin/startup.sh'
            }
        }
        //Code ends for stage Launch Tomcat Server
        
        
        //Code starts for Deploy War on Tomcat Server
        stage('Deploy War on Tomcat Server') {
            steps {
                sh 'cp /var/jenkins_home/workspace/verity-devops-ex/target/ExpenseApp-1.war /tmp/apache-tomcat-9.0.20/webapps'
            }
        }
        //Code ends for stage Deploy War on Tomcat Server
        
        //Code starts for stage API Test
        stage('API Test') {
            steps {
                //Change git url below as per your forked github repository URL
                git url: 'https://github.com/mexgas/EMAPITests-ex.git'
                sh 'mvn -Dtest=ExpenseManagerAPITest test'
            }
        }
        //Code ends for stage API Test    
        
        
        //Code starts for stage System Test
        stage('System Test') {
            steps {
                //Change git url below as per your forked github repository URL
                git url: 'https://github.com/mexgas/EMSystemTests-ex.git'
                sh 'mvn -Dtest=ExpenseManagerSystemTest test'
            }
        }
        
        
        // ******ALL CODE TO BE ADDED ABOVE THIS COMMENT******
    }
}