pipeline {
    agent any
    stages {
        
       
        stage("Build image") {
            steps {
                script {
		    checkout scm
                    myapp = docker.build("sucharan/studentsurvey:${env.BUILD_ID}")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                	sh 'docker login -u sucharan -p Roommates@4309'
					myapp.push("${env.BUILD_ID}")
                }
            }
        }        
        stage("UpdateDeployment") {
			steps{
				sh 'kubectl config view'
				sh "kubectl get deployments"
				sh "kubectl set image deployment/hw2dep645 container-0=sucharan/studentsurvey:${env.BUILD_ID}"
			}
		}
    }    
}