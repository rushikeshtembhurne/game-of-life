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
			 sh 'docker build -t gameoflife -f gameoflife-web/Dockerfile .'
			 }
		}

		stage('Push Docker Image'){
		    steps{
                    withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]){
                        sh "docker tag gameoflife ${env.dockerHubUser}/gameoflife:latest"
                        sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                        sh "docker push rishi0921/gameoflife:latest"
		    }    
                }  
		    }


        stage('Deploy To Docker Container'){
		    steps{
			   sh 'docker run -d --name game -p 8070:8070 rishi0921/gameoflife:latest'
			}  
		    }
		}
		
   }

}

