pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'java'
    }
   withMaven() {
 
      bat "mvn clean install"
 
    } 
}
