pipeline {
     agent any
     stages {
         stage('Clean Workspace') {
             steps {
                  deleteDir()                  
             }
         }
         stage('Clone Project') {
             steps {                  
                  checkout scm                  
             }
         }
         stage('Build') {
             steps {                  
                  sh './gradlew clean build'
             }              
             post {
                 always {
                     jiraSendBuildInfo site: 'bashsquad.atlassian.net'
                 }
             }
         }
         stage('SonarQube analysis') {
               steps { 
                    withSonarQubeEnv() {
                    sh './gradlew sonarqube'
               }
          }
        }
     }
 }
