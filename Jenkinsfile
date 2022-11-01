Pipeline {
	agent any 
	tools {
		maven '3.8.6'
	}
	stages{
		stage('Build Maven'){
			steps{
				checkout($class: 'GitSCM', branches: [[name: '*/main]], extensions: [], userRemoteconfigs: [[url:'https://github.com/sunkarnamritish/645hw2']]])
				sh 'man clean install'
			}
		}
		stage('Build Docker Image'){
			steps{
				script{
					docker.build("sucharan/studentsurvey:${env.BUILD_NUMBER}")
				}
			}
		}
		stage('Push Image To Hub'){
			steps{
				script{
				sh "docker login -u sucharan -p Roommates@4309"
				sh "docker push sucharan/studentsurvey:${env.BUILD_NUMBER}"
				}
			}
		}
		stage("Deploying To Kubernetes"){
			steps{
				script{
					sh "kubectl set image deployment/swe654 swe645 swe645=sucharan/studentsurvery:${env.BUILD_NUMBER}"
				}
			}
		}
}