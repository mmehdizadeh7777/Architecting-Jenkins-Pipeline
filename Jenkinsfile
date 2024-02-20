pipeline {
    
   agent {
        label 'none'
    }

    tools {
      maven 'maven3'
    }
    
    
    stages{
        stage ('Checkout') {
	   agent {
        	label 'ssh'
    		}
            steps{
                checkout poll: false, scm: scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mmehdizadeh7777/Architecting-Jenkins-Pipeline.git']])
            }
            
        }
        stage ('Build') {
	agent {
        	label 'java'
    		}
            steps {
                echo "Build Stage is in progress"
                sh 'mvn compile'
            }
            
        }
        stage ('Test'){
	agent {
        	label 'java'
    		}
            steps {
                echo "Test Stage is in progress"
                sh 'mvn test'
            }
            
        }
        stage('Deploy'){
		agent {
        		label 'ssh'
    		}
            input {
              message 'Do you want to deploy build?'
              ok 'Yes I want'
              parameters {
                string description: 'Who is Approver?', name: 'Approver'
              }
            }
            steps{
                echo 'Deploying Build'
            }
        }
    }
}
