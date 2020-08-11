pipeline {
 agent any
  stages {
    stage('SCM') {
      steps {
         git 'https://github.com/shanmuk98/angular7-sample.git'
       }
    }
   stage("Install node modules") {
     steps {
	     powershell 'npm install'
         echo "modules installed"
   }
   }
   stage("build") {
     steps {
			powershell 'npm run ng -- build --prod'
            echo "build successful"
   }
   }



   stage('Approval') {
            // no agent, so executors are not used up when waiting for approvals
            agent none
            steps {
                script {
                    def deploymentDelay = input id: 'Deploy', message: 'Deploy to production?', submitter: 'rkivisto,admin', parameters: [choice(choices: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24'], description: 'Hours to delay deployment?', name: 'deploymentDelay')]
                    sleep time: deploymentDelay.toInteger(), unit: 'HOURS'
                }
            }
        }
	
    stage('Build images') {
	      steps {
		bat '''
			  docker build -f "Dockerfile" -t prahaskattimani/ng7:latest .
		'''
	      }
       }
   
     stage('Push Docker image') {
[10:45, 01/08/2020] Prahas k(pratian): stage('Push Docker image') {
	  steps{
		    withDockerRegistry([ credentialsId: "Docker_Hub", url: "" ]){
			
			bat "docker push prahaskattimani/ng7:latest"   
	  	   }
	   }
       } 
  }
}
