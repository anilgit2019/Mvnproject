pipeline{
     agent { label 'master' }
    
    tools {
        maven 'maven'
    }
    
    environment {
        GIT_CRED = credentials('github')
    }
    
    options {
        buildDiscarder(logRotator(numToKeepStr: '2')) 
        
    }
    
    parameters {
        string(name: 'SONAR_RUN' , defaultValue: 'no', description: 'run sonar: yes')
        string(name: 'SONAR_TOKEN' , defaultValue: '999999999999', description: 'sonartkn')
    }
    
    stages {

	    
        stage ('build') {
		input { message 'this is QA job'}		
			
            	agent { docker { image 'maven:latest' } }
            	steps { 
               	 sh 'mvn clean install -DskipTests=false'
            	}
        }
        
        stage ('sonar') {
		
    		parameters {
        		string(name: 'SONAR_RUN' , defaultValue: 'no', description: 'run sonar: yes')
        		string(name: 'SONAR_TOKEN' , defaultValue: '999999999999', description: 'sonartkn')
    		}
           
            when {   
                expression { SONAR_RUN  == 'yes' }
            }
			
            steps {
                sh 'printenv'
                sh 'mvn test'
                sh 'mvn sonar:sonar \
                    -Dsonar.projectKey=payments \
                    -Dsonar.host.url=http://ip172-18-0-65-bkm6sdpt0o8g00evelr0-9000.direct.labs.play-with-docker.com \
                    -Dsonar.login=$SONAR_TOKEN'
            }
        }
        
    }
    
    post {
        always { 
            
            junit '**/target/surefire-reports/*.xml'
        }
    }
} 
