pipeline {
    agent any
    
    stages {
        stage("compile code") {
            steps {
                checkout scm
            }
        }
        
        stage("Docker Ops") {
            steps {
                script {
                    ourapp = docker.build("sucharan/ss:${env.BUILD_ID}")
		    sh 'docker login -u Sucharan -p Roommates@4309'
		    ourapp.push("${env.BUILD_ID}")
                }
            }
        }
                
        stage("UpdateDeployment") {
          steps{
            sh 'kubectl config view'
            sh "kubectl get deployments"
            sh "kubectl set image deployment/subhakar.war container-0=sucharan/ss:${env.BUILD_ID}"
          }
		    }
    }    
}