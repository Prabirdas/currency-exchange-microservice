//Scripted

//node {
//	stage('Build') {
	//	echo "Build"
	//}
	//stage('Test') {
		//echo "Test"
	//}
	//}
	
	//Declarative
	
	pipeline{
		agent any
		//agent { docker { image 'maven:3.6.3'}}
		environment{
			dockerHome = tool 'My_Docker'
			mavenHome = tool 'My_Maven'
			PATH = "$dockerHome/bin:$mavenHome/bin:%PATH"
		}
		stages{
			stage('Build'){
				steps{
					echo "Build--echo"					
					sh 'docker version'
					echo "PATH -- $PATH"
					sh 'mvn --version'
					echo "BUILD_ID  --- $env.BUILD_ID"
					echo "BUILD_NUMBER  --- $env.BUILD_NUMBER"
					}
				}
			stage('Test'){
				steps{
					echo "Test"
					}
				}
			}

		post{
			always{
				echo "I am awesome"
				}
			success{
				echo "I run when you are successful"
				}
			failure{
				echo "I run when you fail"
				}
			//changed{}
			}
	}
