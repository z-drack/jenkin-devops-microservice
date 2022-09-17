pipeline {
	agent any
	//agent { docker {image "maven:3.6.3"}}
	stages{
		stage("Build"){
			steps{
				//sh "mvn --version"
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"

			}
		}
		stage("Test"){
			steps{
				echo "Test"
			}
		}
		stage("Integration Test"){
			steps{
				echo "Integration Test"	
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