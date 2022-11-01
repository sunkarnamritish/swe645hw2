pipeline {
    agent any
    environment {
        PROJECT_ID = '645hw2'
        CLUSTER_NAME = '645hw2'
        LOCATION = 'us-east-1a'
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage('BuildWAR') {
            steps {
            
            	dir('src/main/webapp') {
            		echo 'Creating the Jar ...'
					sh 'java -version'
					sh 'jar -cvf subhakar.war *'
            	}
            }
        }
        
        stage("Build image") {
            steps {
                script {
                    myapp = docker.build(“sucharan/645hw2:${env.BUILD_ID}")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                	sh 'docker login -u Sucharan -p Roommates@4309'
					myapp.push("${env.BUILD_ID}")
                }
            }
        }        
        stage("UpdateDeployment") {
			steps{
				sh 'kubectl config view'
				sh "kubectl get deployments"
				sh "kubectl set image deployment/swe645deployment container-0=sucharan/645hw2:${env.BUILD_ID}"
			}
		}
    }    
}