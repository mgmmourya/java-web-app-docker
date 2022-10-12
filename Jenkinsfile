pipeline{
    agent any
    tools{
        maven "maven_3.8.4"
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
    }//stages closing
}//pipeline closing
