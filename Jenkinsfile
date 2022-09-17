pipeline {
	agent any
	//agent { docker {image "maven:3.6.3"}}
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages{
		stage("Checkout"){
			steps{
				sh "mvn --version"
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"

			}
		}
		stage("Compile"){
			steps{
				sh "mvn clean compile"
			}
		}
		stage("Test"){
			steps{
				echo "mvn test"
			}
		}
		stage("Integration Test"){
			steps{
				echo "mvn failsafe:integration-test failsafe:verify"	
			}
		}
		stage("Package"){
			steps{
				echo "mvn package -DskipTest"	
			}
		}
		stage("Build Docker Image"){
			steps{
				// docker build -t kls67/currency-exchange-devops:$env.BUILD_TAG
				script{
					dockerImage = docker.build("kls67/currency-exchange-devops:${$env.BUILD_TAG}")
				}
			}
		}
		stage("Push Docker Image"){
			steps{
				script{
					docker.withRegistry('','dockerhub')
					dockerImage.push();
					dockerImage.push("latest");
				}
			}
		}
	}
	post{
		always {
			echo "I'm awesome, I run always"

		}
		success{
			echo "I run when you success"

		}
		failure{
			echo "I run when you fail"
		}
		//changed: Quando o estado do pipeline muda(funciona -> n funciona; n funciona -> funciona)

	}
}