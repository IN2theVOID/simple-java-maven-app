pipeline {
    agent {
        docker {
            image 'maven:3.8.1-adoptopenjdk-11' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
	options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }

		stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
		stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
		stage('Upload to Nexus'){
			steps {
		
			  
				//nexusArtifactUploader {
					
				//	nexusVersion('nexus2')
				//	protocol('http')
				//	nexusUrl('nexus:8081')
				//	groupId('sberChallenge')
				//	version('2.4')
				//	repository('maven-public')
				//	credentialsId('nexus')
				//	artifact {
				//		artifactId('nexus-artifact-uploader')
				//		type('jar')
				//		classifier('debug')
				//		file('nexus-artifact-uploader.jar')
				//	}
				//	artifact {
				//		artifactId('nexus-artifact-uploader')
				//		type('hpi')
				//		classifier('debug')
				//		file('nexus-artifact-uploader.hpi')
				//	}

				}
			}
		}
	}
