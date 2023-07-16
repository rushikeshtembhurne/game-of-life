pipeline {

   agent {label 'JDK8'}
   
   stages{
		stage('SourceCode'){
		     steps{
			 git branch: 'sprint1_develop', url: 'https://github.com/rushikeshtembhurne/game-of-life.git'
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
   }
}
