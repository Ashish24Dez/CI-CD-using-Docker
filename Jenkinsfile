pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/Ashish24Dez/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
                sh 'mvn clean' 
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t sampleweb:V1.1.04 .' 
                sh 'docker tag sampleweb:V1.1.04 sampleweb:V1.1.latest'
                //sh 'docker tag samplewebapp ashishut/samplewebapp:$L_1_01'
              
        }
  }
  stage('Publish image to Docker Hub') {
          
            steps {
       withDockerRegistry(url: 'https://hub.docker.com/repository/docker/ashishut/appdep') {
       sh 'sudo docker push sampleweb:V1.1.latest'
}
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 appdep/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 appdep/samplewebapp"
 
            }
        }
    }
}
