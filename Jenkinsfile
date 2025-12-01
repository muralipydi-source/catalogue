pipeline {
    agent {
        label 'AGENT-1'
   }

 //Build
 stages {
    stage('Build') {
            steps {
                script {
                   echo 'Building..'
                }
             }
    }
    stage('Test') {
            steps {
                script {
                echo 'Testing..'
            }
    }
  }
    stage('Deploy') {
            steps {
                script {
                echo 'Deploying....'
            }
        }
    }
    } 
 post { 
        always { 
            echo 'I will always say Hello again!'
                 deleteDir()
        }
        success { 
            echo 'Hello Success'
        }
        failure { 
            echo 'Hello Failure'
        }
   }
}





/* @Library('jenkins-shared-library') _

def configMap = [
    project : "roboshop",
    component: "catalogue"
]

if( ! env.BRANCH_NAME.equalsIgnoreCase('main') ){ // if not equals to main
    nodejsEKSPipeline(configMap) // by default it will call, call function inside this pipeline
}
else{
    echo "Please proceed with PROD process"
}
 */