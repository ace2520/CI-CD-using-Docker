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
              
                sh 'docker build -t mystery/samplewebapp:latest .' 
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
      withCredentials([string(credentialsId: '4f9d1c9c-3896-4743-b2f9-9c3fb3af7eef', variable: 'pwd')]) {
	      sh "docker login -u mystery48 -p ${pwd}" 
        }
	      sh "docker push mystery48/samplewebapp"
	    }
                  
          }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 8003:8080 mystery48/samplewebapp"
 
            }
        }
// stage('Run Docker container on remote hosts') {
             
          //  steps {
             //   sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 nikhilnidhi/samplewebapp"
 
 //           }
   //     }
    }
}
