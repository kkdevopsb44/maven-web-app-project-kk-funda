pipeline {
    agent any 
tools
{
  maven "maven3.9.9"
}

    stages {
        stage('checkout stage') { 
            steps {
           git branch: 'jenkins', credentialsId: '8d341570-e046-4d2c-8060-33c3d5d493f7', url: 'https://github.com/gangavaramdevops/maven-web-app-project-kk-funda.git'
            }
        }
            stage('Build') { 
            steps {
         sh "mvn clean package"

            }
          }
          stage('SQREPORT'){
            steps{
          sh "mvn sonar:sonar"
          }
        }
         stage('DeployTONexus'){
           steps{
          sh "mvn deploy"
          }
        }
        stage('DeployAppToTomcat'){
           steps{

        echo "Deploying WAR file using curl..."

        sh """
            curl -u kkfunda:kkfunda \
            --upload-file /var/lib/jenkins/workspace/jio-scripted-way-pipeline-develoment/target/maven-web-application.war \
            "http://3.108.194.157:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """

          }
        }
    } //stages closing

post {
  success {
    notifyBuild(currentBuild.result)
  }
  failure {
notifyBuild(currentBuild.result)
      }
}
}//pipeline closing


def notifyBuild(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary, channel: '#jio-project')
}
