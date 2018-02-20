node () {
  
   if  (env.BRANCH_NAME == 'master') {
     echo "checkout for branch"+env.BRANCH_NAME   
     checkout()
        build()            
    } 
    else { 
    }
   echo "checkout for branch"+env.BRANCH_NAME   
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
