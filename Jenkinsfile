def readProb;
		
	def FAILED_STAGE
	pipeline {
	agent any
	stages {
	    stage('Setup'){
	    steps {
	        script {
	        readProb = readProperties  file:'testconfig.properties'
	        FAILED_STAGE=env.STAGE_NAME
	        Setup= "${readProb['Setup']}"
			if ("$Setup" == "yes") {
		 sh "git config --global user.email asakthivel72@hotmail.com"
	        sh "git config --global user.name ${readProb['user.name']}"
	        sh 'git config --global credential.helper cache'
	        sh 'git config --global credential.helper cache'
	        sh "if [ -d ${readProb['Project_name']} ]; then rm -Rf ${readProb['Project_name']}; fi"
	        sh "if [ -d ${readProb['PMD_result']} ]; then rm -Rf ${readProb['PMD_result']};  fi"        
	        sh "mkdir ${readProb['PMD_result']}"
			}
			else {
			 echo "Skipped stage"
			}
			}
		}
		}
		
	stage('Git Pull'){
        steps {	dir("${readProb['Project_name']}"){
		 git branch: "${readProb['branch']}", credentialsId: "${readProb['credentials']}", url: "${readProb['GITHUB_URL']}"    
	      }
		}
		}
		
		
		}
	}
