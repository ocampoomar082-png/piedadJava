pipeline {
    agent any

tools {
    nodejs "node"
  }

     stages {
        stage('install') {
      steps {
	    deleteDir()
        git branch: 'main', credentialsId: 'github_1', url: 'https://github.com/ocampoomar082-png/piedadJava.git'
		 dir('frontend') {
          bat 'npm install'
        }
        }
      }
    
          stage('Unit-test') {
      steps {
        dir('frontend') {
          bat 'npm run test'
        }
      
	  
	  
	  }
	  stage('build') {
      steps {
        dir('frontend') {
          script {
		   bat 'npm run build'
          
            
              
            }
          }
         
        }
      }
    
    
	}//Fin stages
}//Fin Pipeline

