node () {
  
   if  (env.BRANCH_NAME == 'develop') {
     echo "checkout for branch=============================================="+env.BRANCH_NAME   
     build()
               
    } 
    else { 
     checkout() 
    }
    
 checkout()
}

def checkout(){
 stage 'Checkout code'
    context="continuous-integration/jenkins/"
    context +="branch/checkout"
    checkout scm
}

def build(){
 stage ('Build') {
  echo "starting building=========================================================="
    withMaven() {
 
      bat "mvn clean install -DskipTests=true -Dmaven.javadoc.skip=true -Dcheckstyle.skip=true -B -V"
 
    } 
  }
}
