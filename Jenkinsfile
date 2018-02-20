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
     buildInfo = Artifactory.newBuildInfo()
     buildInfo.env.capture = true
    
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
     }
}

def checkout () {
    stage 'Checkout code'
    context="continuous-integration/jenkins/"
    context += "branch/checkout"
    checkout scm
    setBuildStatus ("${context}", 'Checking out completed', 'SUCCESS')
}

def build () {
    stage 'Build'
    mvn 'clean install -DskipTests=true -Dmaven.javadoc.skip=true -Dcheckstyle.skip=true -B -V'
}
