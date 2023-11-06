pipeline{
	agent{
		label 'Jenkins-Agent'
		}
	
	tools{
		jdk 'Java17'
		maven 'Maven3'
		}
		
	stages{
		stage("Cleanup Workspace"){
			steps{
				cleanWs()
				}
			}
			
		stage("Checkout from SCM"){
			steps{
				git branch: 'master', credentialsId: 'github', url: 'https://github.com/XI2877-IndrajeetMagdum/register-app'
				}
			}
			
		stage("Build Application"){
			steps{
				sh "mvn clean package"
				}
			}
			
		stage("Test Application"){
			steps{
				sh "mvn test"
				}
			}
		stage("Soanrqube Analysis"){
			steps{
				script{
				withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token'){
					sh "mvn sonar:sonar"
				         }
				      }
			     }
			}

		stage("Quality Gate"){
			steps{
				script{
					waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonarqube-token'
				}
				sh "mvn test"
				}
			}
	}
}
