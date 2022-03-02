pipeline{

  environment{
  registry = "battiseashish24/learning-pipeline-nodejs"
  registryCredential = "dockerhub"
  dockerImage = ''
  PATH = "$PATH/usr/local/bin"
  
  }
  agent any
  stages{
    stage('Cloning git'){
	  steps{
             git 'https://github.com/ashishbattise24/learning-Jenkins-pipeline.git'	  
	  }
	}
    stage('build docker image'){
	   steps{
	      script{
	       dockerImage = docker.build registry + ":$BUILD_NUMBER" 
		  }
	   }
	
	}
	stage('Push image to docker hub'){
	  steps{
	     script{
		         docker.withRegistry('', registryCredential){
				    dockerImage.push() 
				 }				 
		 }
	  
	  }
	
	}
	stage('cleaning up'){
	  steps{
	        sh "docker rmi $registry:$BUILD_NUMBER"
	  }
	
	}
  }
  


}
