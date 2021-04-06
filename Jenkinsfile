pipeline {
	environment {
		registry = "vancherla/Git-jen-doc"
		registryCredential = 'dockerhub'
		dockerImage = ''
		dockerRunCommand = 'docker run -d -p 8080:8080 -name myapp vancherla/Git-jen-doc'
	}
	agent any
	stages {
		stage("Building docker image") { 
			steps {
				script {
					dockerImage = docker.build registry + ":$BUILD_NUMBER"
				}
			}
		}
		stage("Pushing image to DockerHub") { 
			steps {
				script {
					docker.withRegistry( '', registryCredential ) {
						dockerImage.push()
						dockerImage.push( 'latest' )
					}
				}
			}
		}
	}
}
