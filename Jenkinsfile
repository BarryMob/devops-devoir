node {
    // reference to maven
    // ** NOTE: This 'maven-3.5.2' Maven tool must be configured in the Jenkins Global Configuration.   
    def mvnHome = tool 'maven-3.8.1'

    // holds reference to docker image
    def dockerImage
 
    def dockerImageTag = "devoirDevOps${env.BUILD_NUMBER}"
    
    stage('Clone Repo') { // for display purposes
      // Get the code from my GitHub repository
      git 'https://github.com/BarryMob/devops-devoir.git'
      // Get the Maven tool.
      mvnHome = tool 'maven-3.8.1'
    }    
  
    stage('Build Project') {
      // build project via maven
      sh "'${mvnHome}/bin/mvn' clean install"
    }
		
    stage('Build Docker Image') {
      // build docker image
      dockerImage = docker.build("devoirDevOps:${env.BUILD_NUMBER}")
    }
   
    stage('Deploy Docker Image'){
      
      // deploy docker image to nexus
		
      echo "Docker Image Tag Name: ${dockerImageTag}"
	  
	  sh "docker stop devoirDevOps"
	  
	  sh "docker rm devoirDevOps"
	  
	  sh "docker run --name devoirDevOps -d -p 2222:2222 devoirDevOps:${env.BUILD_NUMBER}"
	  
	  // docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
      //    dockerImage.push("${env.BUILD_NUMBER}")
      //      dockerImage.push("latest")
      //  }
      
    }
}