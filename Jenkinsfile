#!groovy
import groovy.json.JsonOutput
import groovy.json.JsonSlurper
pipeline {
    agent any
    tools { 
        maven 'maven' 
        jdk 'java' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }

        stage ('Build') {
            steps {
                echo 'This is a minimal pipeline.'
            }
        }
    }
}
