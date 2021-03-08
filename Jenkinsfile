pipeline {
    agent any
	
	  tools
    {
        maven 'Maven'
        jdk 'jdk' 
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/arunsaxena01/Docker-Demo.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t dockerdemocasestudy:latest .' 
                sh 'docker tag dockerdemocasestudy manivannanmari/dockerdemocasestudy:latest'              
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerMani", url: "" ]) {
          sh  'docker push manivannanmari/dockerdemocasestudy:latest' 
        }
                  
          }
        }
     
   /*   stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 manivannanmari/dockerdemocasestudy"
 
            }
        } 
  */
 stage('Run Docker container on remote hosts') {
             
            steps {
                //sh "docker -H ssh://root@52.255.157.89 run -d -p 8003:8080 manivannanmari/samplewebapp"
                //sh "docker -H ssh://root@35.174.204.80 run -d -p 8081:8080 manivannanmari/dockerdemocasestudy"
              //  sh "docker -H ssh://jenkins@100.25.118.2 run --privileged -p 8081:8080 manivannanmari/samplewebapp"
 		echo "Printing "
            }
        } 
    stage('Deploy App in Kuberneter cluster') {
             
            steps {
               withCredentials([usernamePassword(credentialsId: 'acr-credentials', usernameVariable: 'ACR_ID', passwordVariable: 'ACR_PASSWORD')]) {
		//sh 'kubectl apply -f deployment.yaml'	
		 //sh 'kubectl set image -n default deployment/myapp myapp=manivannanmari/dockerdemocasestudy:latest'  
		 echo 'kubectl set image -n default deployment/myapp myapp=manivannanmari/dockerdemocasestudy:latest'
		}
 
            }
        } 	 
    }
	}
