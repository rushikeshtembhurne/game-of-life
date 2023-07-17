pipeline {

   agent {label 'JDK8'}
   
   stages{

		stage('SourceCode'){
		     steps{
			 git branch: 'sprint1_develop', url: 'https://github.com/rushikeshtembhurne/game-of-life.git'
			 }
		}
		stage('Code Compile'){
		    steps{
		    sh 'mvn clean compile'  
		    }
		}
		stage('Build the code'){
		    steps{
		    sh 'mvn clean package'  
		    }
		}

		stage('Archiving the Test Results'){
		     steps{
			 junit '**/surefire-reports/*.xml'
			 archiveArtifacts artifacts: '**/*.war', followSymlinks: false
			 }
			 
		}
		stage('Build Docker Image'){
		    steps{   
			 sh 'docker build -t gameoflife .'
			 }
		}

		stage('Push Docker Image'){
		    steps{
                    withCredentials([usernamePassword(credentialsId:'docker',usernameVariable:'dockerUser',passwordVariable:'dockerPass')]){
                        sh 'docker tag gameoflife ${env.dockerUser}/gameoflife:latest'
                        sh 'docker login -u ${env.dockerUser} -p ${env.dockerPass}'
                        sh 'docker push rishi0921/gameoflife:latest'
                    }      
                }  
		    }


        stage('Deploy To Docker Container'){
		    steps{
		       script {
			   withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
					sh 'docker run -d --name game -p 8070:8070 rishi0921/gameoflife:latest'
				}
			   }  
		    }
		}
		
   }

}

