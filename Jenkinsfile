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
              
                sh 'docker build -t sampleweb:V1.1.02 .' 
                sh 'docker tag samplewebapp ashishut/samplewebap:V1.1.01'
                //sh 'docker tag samplewebapp ashishut/samplewebapp:$L_1_01'
              
        }
  }
  stage('Publish image to Docker Hub') {
          
            steps {
       withDockerRegistry(credentialsId: '46e65d3d-5b03-4e93-aef3-6e8fdf58ef1f', toolName: 'Docker', url: 'https://hub.docker.com/repository/docker/ashishut/appdep') {
       sh 'docker push ashishut/appdep:LV_1_01'
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
