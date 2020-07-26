pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mymaven"
		jdk "jdk1.8.0_251"
    }
    stages {
        stage('Remove the CodeBase folder') {
            steps {
                
                echo 'test'
                bat "mvn clean "
            }
        }
        stage('Pull from a specific branch') {
            steps {
                
                git branch: 'Test', credentialsId: 'gut8SqLEVbG4EPbktuygUjeo', url: 'https://github.com/sakthivel72/DevOpsClassCodes.git'
            }
        }
        stage('Compile and unit test using Maven') {
            steps {
               
              script {
                env.RELEASE_SCOPE = input message: 'User input required', ok: 'Release!',
                        parameters: [choice(name: 'RELEASE_SCOPE', choices: 'patch\nminor\nmajor', 
                                     description: 'What is the release scope?')]
            
            echo "${env.RELEASE_SCOPE}"
            if (env.RELEASE_SCOPE == 'patch') {
            bat "mvn clean package" }
            else {
            echo 'else' } }
            
            }
        }
         stage('Deploy the packageDeploy') {
            steps {
                
                 echo 'mvn package'
                 bat "mvn clean install"
                   }
		}	
             stage('Slack notification') {
            steps {
                 slackSend channel: 'jenkin', message: 'job completed ', tokenCredentialId: 'jenkins'
            }
        
        }
    }
}
