pipeline {
    agent any
	
	  tools
    {
       maven "maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/velpularajeswari/WebApplication'
             
          }
        }
	 stage('Package') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build') {
           steps {
              
                sh 'docker build -t rajeswari/maven-app:1.0.0 .' 
               
          }
        }
     
  stage('Publish Image') {
          
            steps {
        withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerpwd')]) {
                 sh "docker login -u rajeswari1994 -p ${dockerpwd}"
                 sh 'docker push rajeswari1994/maven-app:1.0.0' 
        }
                  
          }
        }
     
      stage('Run Docker container') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 rajeswari1994/maven-app:1.0.0"
 
            }
        }
     }
	}
    
