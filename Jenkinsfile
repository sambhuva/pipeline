node () {
  
   if  (env.BRANCH_NAME == 'master') {
        checkout()
        build()            
    } 
    else { 
    }
 checkout()
}

def checkout(){
 stage 'Checkout code'
    context="continuous-integration/jenkins/"
    context +="branch/checkout"
    checkout scm
  echo "checkout done"
}

def build(){
 stage ('Build') {
  echo "starting building"
    withMaven() {
 
      bat "mvn clean install"
 
    } 
  }
}
