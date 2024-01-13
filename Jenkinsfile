/* import shared library */
@Library('jenkins-shared-library')_

pipeline {
    agent any
    stages {
       stage('Check Syntax - Dockerfile'){
          steps{
             script {
                 script { dockerfileCheck }
                   
               }
            }
          }
       stage('Check Python  syntax') {
           agent any
            steps {
             script { pythonCheck }
            }
        }
       stage('Check Sql syntax') {
           agent any
            steps {
             script { sqlCheck }
            }
        }

        stage('Check Golang syntax') {
            agent any
            steps {
             script { golangCheck }
            }
        }
   
       stage('Check NodeJs syntax') {
            agent { 
                docker { 
                    image 'node:latest'
                    args '-u root:root'
                } 
            }
            steps {
                sh 'npm install -g jshint'
                sh 'npm install --save-dev jshint'
                sh 'jshint  \${WORKSPACE}/battleboat/js/battleboat.js'
            }
        } 
        
       /*  stage('Check Css syntax') {
            agent { docker { image 'hspaans/csslint' } }
            steps {
             script { cssCheck }
            }
        } */
        /*stage('SonarQube analysis') {
             agent {
                 docker {
                 image 'sonarsource/sonar-scanner-cli:4.8'
               }
             }
                environment {
           CI = 'true'
           scannerHome='/opt/sonar-scanner'
    }
          steps{
               withSonarQubeEnv('Sonarqube') {
                 sh "${scannerHome}/bin/sonar-scanner"
            }
          }
       }
       stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true }
            }
        }*/

    }
    post {
    always {
       script {
         /* Use slackNotifier.groovy from shared library and provide current build result as parameter */
         clean
         slacknotifier currentBuild.result
     }
    }
    }
}
