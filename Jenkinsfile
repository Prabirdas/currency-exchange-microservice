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
			PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
		}
		stages{
			stage('Checkout'){
				steps{
					echo "Build--echo"					
					sh 'docker version'
					sh 'mvn --version'
					echo "PATH -- $PATH"
					echo "BUILD_ID  --- $env.BUILD_ID"
					echo "BUILD_NUMBER  --- $env.BUILD_NUMBER"
					echo "BUILD TAG  --- $env.BUILD_TAG"
					}
				}
			stage('Compile'){
				steps{
					sh "mvn clean compile"
				}
			}
			stage('Test'){
				steps{
					echo "Test"
					}
				}
			stage('Package'){
				steps{
					sh "mvn package -DskipTests"
					}
				}
				
			stage('Build Docker image'){
				steps{
					//"docker build -t prabirdos/currency-exchange-devopps:$env.BUILD_TAG"
					script{
						dockerImage = docker.build("prabirdos/currency-exchange-devopps:${env.BUILD_TAG}")
						}
					}
				}
			stage('Push Docker image'){
				steps{
					script{
						docker.withRegistry('','dockerHub'){
							dockerImage.push();
							dockerImage.push('latest');
							}
						}
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
