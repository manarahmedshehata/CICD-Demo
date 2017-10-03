pipeline {
    agent any
    
    stages {
    	
        stage('Java Build') {
			
        	steps {
				notifyStarted("Java Build","Kindly be informed that job started successfully")
   //      		echo "java build"
			// sh"""
			// 	cd ./demo
			// 	mvn clean package
			// """
			        	}
		post
		{
		success{
			notifySuccessful("Java Build","Kindly be informed that code build is done successfully")
 			}
        failure{
        	notifyFailed("Java Build")
//             	emailext attachLog: true, subject: 'Jenkins job Java build failed', to: 'manar.hassan1@vodafone.com,yara.abdellatif1@vodafone.com,Ahmed.Said-AbdAllah2@vodafone.com', body: """
// Dears,

// Kindly be informed that the job java build has failed, please find the logs attached to this email.
			
// Thanks
// Deployment CoE
// """
        	 }
    	}

        }
	   
        stage('docker Build') {
		steps {
			notifyStarted("Docker Build","Kindly be informed that job started successfully")
			echo "docker build"
	/*		
			withCredentials([usernamePassword(credentialsId: '18b57317-0966-4f4a-9fa8-49f733bc09bd', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
				sh """
				cd demo/src/main/docker/
				cp ${WORKSPACE}/demo/target/employees-app-1.0-SNAPSHOT-jar-with-dependencies.jar .
				docker build -t deploymentcoe/cicd-demo .
				docker login --username $USERNAME --password $PASSWORD
				docker push deploymentcoe/cicd-demo
				docker images
				docker rmi deploymentcoe/cicd-demo
				
				"""
			}
				
		}
		*/
		post
		{
		success{
			notifySuccessful("Docker Build","Kindly be informed that code is containerized and Docker image is ready to be use")
// 				mail (to: 'yara.abdellatif1@vodafone.com,manar.hassan1@vodafone.com,Ahmed.Said-AbdAllah2@vodafone.com',
//                 		subject: "Jenkins Job Docker success",
//                 		body: """
// Dears,

// Kindly be informed that code is containerized and Docker image is ready to be used.
			
// Thanks
// Deployment CoE
// 					""");
			}
//         failure{
//             	emailext attachLog: true, subject: 'Jenkins Job Docker build failed', to: 'manar.hassan1@vodafone.com,yara.abdellatif1@vodafone.com,Ahmed.Said-AbdAllah2@vodafone.com', body: """
// Dears,

// Kindly be informed that the job docker build has failed, please find the logs attached to this email.
			
// Thanks
// Deployment CoE
// """
//         	}
    	}
			
			
        	}

        stage('Deployment') {
			steps {
				notifyStarted("Kubernetes Deployment","Kindly be informed that job started successfully")
				echo "Deployment"
	/*		
				sh """
					kubectl delete -f ./manifests/deployment.yaml
					#kubectl delete -f ./manifests/ingress.yaml
					kubectl apply -f ./manifests

					
				 """		
        	}
        	*/
        	post
			{
			success{
				notifySuccessful("Kubernetes Deployment","Kindly be informed that Kubernetes deployment is completed and micro service is ready to test")
// 				mail (to: 'yara.abdellatif1@vodafone.com,manar.hassan1@vodafone.com,Ahmed.Said-AbdAllah2@vodafone.com',
//                 		subject: "Jenkins Job Deployment success",
//                 		body: """
// Dears,

// Kindly be informed that code is containerized and Docker image is ready to be used.
			
// Thanks 
// Deployment CoE
// 					""");
			}
//         failure{
//             	emailext attachLog: true, subject: 'Jenkins job Kubernetes deployment failed', to: 'manar.hassan1@vodafone.com,yara.abdellatif1@vodafone.com,Ahmed.Said-AbdAllah2@vodafone.com', body: """
// Dears,

// Kindly be informed that the job docker build has failed, please find the logs attached to this email.
			
// Thanks
// Deployment CoE
// """
//         	}
    	}
    	
        }
/*
    	stage('Failed Job') {
			steps {

				sh 'cd nothing'
				
        	}
        post
		{
		success{
				mail (to: 'yara.abdellatif1@vodafone.com,manar.hassan1@vodafone.com,Ahmed.Said-AbdAllah2@vodafone.com',
                		subject: "Jenkins",
                		body: """
Dears,

Kindly be informed that the job is successful.
			
Thanks
Deployment CoE
					""");
			}
        failure{
            	emailext attachLog: true, subject: 'Jenkins job failed test', to: 'manar.hassan1@vodafone.com,yara.abdellatif1@vodafone.com,Ahmed.Said-AbdAllah2@vodafone.com', body: """
Dears,

Kindly be informed that the job has failed, please find the logs attached to this email.
			
Thanks
Deployment CoE
"""
        	}
    	}
        }
*/
    }

}


//functions

def notifyStarted(stagename,mailbody) {
	// send to Slack
  slackSend (color: '#FFFF00', message: "STARTED: Job $stagename '[${env.BUILD_NUMBER}]'")
  mail (to: 'yara.mohamed174@gmail.com',
                		subject: "Jenkins Job ${env.JOB_NAME} $stagename [${env.BUILD_NUMBER}] success",
                		body: """
Dears,

$mailbody .
			
Thanks
Deployment CoE
					"""); 
}

def notifySuccessful(stagename,mailbody) {
  slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' ")
  mail (to: 'yara.mohamed174@gmail.com',
                		subject: "Jenkins Job ${env.JOB_NAME} $stagename [${env.BUILD_NUMBER}] success",
                		body: """
Dears,

$mailbody .
			
Thanks
Deployment CoE
					""");
 }

def notifyFailed(stagename) {
  slackSend (color: '#FF0000', message: "FAILED: Job $stagename' [${env.BUILD_NUMBER}]'")
  emailext attachLog: true, subject: 'Jenkins job ${env.JOB_NAME} $stagename [${env.BUILD_NUMBER}] failed', to: 'yara.mohamed174@gmail.com', body: """
Dears,

Kindly be informed that the job $stagename has failed, please find the logs attached to this email.
			
Thanks
Deployment CoE
"""
}
