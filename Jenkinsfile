#!groovy
import groovy.json.JsonOutput
import groovy.json.JsonSlurper

/*
Please make sure to add the following environment variables:
HEROKU_PREVIEW=<your heroku preview app>
HEROKU_PREPRODUCTION=<your heroku pre-production app>
HEROKU_PRODUCTION=<your heroku production app>
Please also add the following credentials to the global domain of your organization's folder:
Heroku API key as secret text with ID 'HEROKU_API_KEY'
GitHub Token value as secret text with ID 'GITHUB_TOKEN'
*/


pipeline {
    agent any
   tools {
        maven 'maven'
        jdk 'java'
    }
 
        //do some stuff, run your tests, etc.            
   
    // pull request or feature branch
    if  (env.BRANCH_NAME == 'master') {
        
        checkout()
       build ()
       
    } 
   
}

def checkout () {
    stage 'Checkout code'
     context="continuous-integration/jenkins/"
    context += "branch/checkout"
    checkout scm
   
}

def build () {
 stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

       
    
  stage ('Build'){
   steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            }
  }
 }
}
