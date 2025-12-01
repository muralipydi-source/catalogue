pipeline {
    agent {
        label 'AGENT-1'
   }

   environment {
       appVersion = ''
       REGION = 'us-east-1'
       ACC_ID = '898080060887'
       PROJECT = 'roboshop'
       COMPONENT = 'catalogue'
   }
 //Build
 stages {
    stage('Read package.json') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version //echo "Project Name: ${packageJson.name}"
                    echo "Package Version: ${appVersion}"

                    // Accessing a script, for example
                   // if (packageJson.scripts && packageJson.scripts.test) {
                     //   echo "Test script: ${packageJson.scripts.test}"
                    //}
                }
            }
    }
    stage('Install Dependencies') {
            steps {
                script {
                      sh """
                         npm install
                      """

                    // Accessing a script, for example
                   // if (packageJson.scripts && packageJson.scripts.test) {
                     //   echo "Test script: ${packageJson.scripts.test}"
                    //}
                }
            }
    }

    stage('Docker Build & Push') {
    steps {
        script {
            withAWS(credentials: 'aws-credentials', region: "${REGION}") {
                sh """
                    aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com
                    
                    docker build -t ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion} .

                    docker push ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion}
                """
            }
        }
    }
}
    /* stage('Docker Build') {
            steps {
                script {
                      withAWS(credentials: 'aws-credentials', region: ${REGION}) {
                       sh """
                           aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com
                           docker build -t ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com/${PROJECT}/$COMPONENT}:${appVersion}
                           docker push ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com/${PROJECT}/$COMPONENT}:${appVersion}
                      """
                      }
                }
            }
    } */
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