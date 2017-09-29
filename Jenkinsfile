pipeline {
    agent any
    stages {
        stage('Java Build') {
        	steps {
			
        		echo "java build"
        		/*
			sh"""
				cd ./demo
				mvn clean package
			"""
			*/
        	}
        }
	    
        stage('docker Build') {
		steps {
			echo "docker build"
			// withCredentials([usernamePassword(credentialsId: '18b57317-0966-4f4a-9fa8-49f733bc09bd', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
			// 	sh """
			// 	cd demo/src/main/docker/
			// 	cp ${WORKSPACE}/demo/target/employees-app-1.0-SNAPSHOT-jar-with-dependencies.jar .
			// 	docker build -t deploymentcoe/cicd-demo .
			// 	docker login --username $USERNAME --password $PASSWORD
			// 	docker push deploymentcoe/cicd-demo
			// 	docker images
			// 	docker rmi deploymentcoe/cicd-demo
				
			// 	"""
				
			// }
			
			
        	}
        }

        stage('Deployment') {
			steps {
				echo "Deployment"
				sh """
					kubectl delete -f ./manifests/deployment.yaml
					kubectl delete -f ./manifests/ingress.yaml
					kubectl apply -f ./manifests

					
				"""
				//deleteDir()
				
        	}
        }

    }
}
