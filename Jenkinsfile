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
    //env.JAVA_HOME="${tool 'jdk18151'}"
   // env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
    
    // pull request or feature branch
    if  (env.BRANCH_NAME != 'master') {
        checkout()
        build()
      
    } // master branch / production
    else { 
       
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

def mvn(args) {
    withMaven(
        // Maven installation declared in the Jenkins "Global Tool Configuration"
        maven: 'Maven 3.x',
        // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
        
        // settings.xml referencing the GitHub Artifactory repositories
         mavenSettingsConfig: '0e94d6c3-b431-434f-a201-7d7cda7180cb',
        // we do not need to set a special local maven repo, take the one from the standard box
        //mavenLocalRepo: '.repository'
        ) {
        // Run the maven build
        sh "mvn $args -Dmaven.test.failure.ignore"
    }
}

def getBranch() {
    tokens = "${env.JOB_NAME}".tokenize('/')
    branch = tokens[tokens.size()-1]
    return "${branch}"
}
}
