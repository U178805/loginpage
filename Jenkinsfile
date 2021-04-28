pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devops4solutions/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp vipinchechi/loginpage_project:latest'
                //sh 'docker tag samplewebapp vipinchechi/loginpage_project:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "test", url: "" ]) {
          sh  'docker push vipinchechi/loginpage_project:latest'
        //  sh  'docker push vipinchechi/loginpage_project:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8004:9090 vipinchechi/loginpage_project:latest"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh jenkins@192.168.56.103 run  -p 8004:9090 vipinchechi/loginpage_project"
 
            }
        }
    }
	}
    
