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

node {

     server = Artifactory.server "ART"
     buildInfo.env.capture = true
     rtMaven = Artifactory.newMavenBuild()
       
    
    // we need to set a newer JVM for Sonar
    env.JAVA_HOME="${tool 'java'}"
    env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
     try {
        //do some stuff, run your tests, etc.            
   
    // pull request or feature branch
    if  (env.BRANCH_NAME == 'master') {
        
        checkout()
        build()
       
    } // master branch / production
    else { 
       
    }
     }finally{ println("done");}
}

def checkout () {
    stage 'Checkout code'
     context="continuous-integration/jenkins/"
    context += "branch/checkout"
    checkout scm
   
}

def build () {
    stage 'Build'
    rtMaven.tool = 'maven' // Tool name from Jenkins configuration
       
    
        rtMaven.run pom: 'pom.xml', goals: ' clean install', buildInfo: buildInfo
        buildInfo = Artifactory.newBuildInfo()
}
