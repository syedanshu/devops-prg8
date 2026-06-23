# devops-prg8
pipeline{
	agent any
	tools{
		maven 'Maven'
		jdk 'JDK17'
	}
	stages{
		stage('Checkout'){
			steps{
				git branch:'main',url:'    '
			}
		}
		stage('Build'){
			steps{
				bat 'mvn clean package'
			}
		}
		stage('Test'){
			steps{
				bat 'mvn test'
			}
		}
	}
	post{
		always{
			junit allowedEmptyResults:true, testResults:'**/target/surefire-reports/*.xml'
		}
	}
}
