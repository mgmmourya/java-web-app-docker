pipeline{
    agent any
    tools{
        maven "maven_3.8.4"
    }
    options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')
}
    triggers {
  pollSCM ('* * * * *')
}
    stages{
        stage("Cloning"){
            steps{

                git credentialsId: '19127c07-7e12-4694-a7b4-fba271c0d208', url: 'https://github.com/mgmmourya/java-web-app-docker.git'
            }
        }
        stage("Build"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("Sonar Report"){
            steps{
                sh "mvn sonar:sonar"
            }
        }
        stage("Uplaod artifacts into artifactory"){
            steps{
                sh "mvn deploy"
            }
        }
          stage("Deploying"){
            steps{
                sshagent(['838ac8d1-b10a-440b-9116-7ee44bf89ec1']){
        sh "scp -o StrictHostKeyChecking=no target/java-web-app-1.0-SNAPSHOT.war ec2-user@3.6.126.248:/opt/tomcat/webapps"
}
            }
        }
    }//stages closing
}//pipeline closing
