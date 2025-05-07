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

    // Stage 3: Deploy WAR to Tomcat using curl
    stage('Deploy to Tomcat') {
        echo "Deploying WAR file using curl..."

        sh """
            curl -u kkfunda:kkfunda \
            --upload-file /var/lib/jenkins/workspace/scripted-pl/target/maven-web-application.war \
            "http://174.129.132.254:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """
    }
}
