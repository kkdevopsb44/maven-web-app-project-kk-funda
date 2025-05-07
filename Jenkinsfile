node{
// Define Maven tool form Jenkins global configuration
def mavenHome = tool name: 'maven3.9.9'    
 // Stage 1: Checkout source code from Git
    stage('git checkout')
  {
    git branch: 'development', credentialsId: '2098ae86-4ac4-410f-89ef-10684fdfdf6f', url: 'https://github.com/kkdevopsb44/maven-web-app-project-kk-funda.git'
  }
// Stage 2: Build the application and package it (.war/.jar)
    stage('Build'){
          sh "${mavenHome}/bin/mvn clean package"
          }

}
