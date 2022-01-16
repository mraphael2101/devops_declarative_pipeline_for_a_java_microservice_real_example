

// A DECLARATIVE PIPELINE

pipeline {	

	agent any

	environment {
		javaHome = tool 'myJDK_11'
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	
	stages {
		stage('Checkout') {
			steps {
				// Example shell scripts in the Groovy file
				sh 'mvn --version'
				sh 'docker version'
				sh 'java -version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
			}
		}
		stage('Build') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
	} 
	post {
		always {
			echo "This block of code will always execute"
		}
		success {
			echo "This block of code only runs if the job is successful"
		}
		failure {
			echo "This block of code only runs if the job fails at a specific step"
		}
	}
}
