pipeline {
   agent any

   environment {
     SERVICE_NAME = "postgres-db"     
     GITCOMMITSHA = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
   }

   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git credentialsId: 'GitHub', url: "https://github.com/${ORGANIZATION_NAME}/${SERVICE_NAME}"
         }
      }

       stage('Deploy to Cluster') {
          steps {
              sh 'kubectl apply -f deploy.yaml'
               }
          }
      }

     
   }