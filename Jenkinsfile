pipeline {
    agent any 
    
    tools {
        maven "MAVEN_HOME"
    }
    
    stages{
        
        stage("Git Checkout"){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mmukul/Petclinic.git'
            }
        }
        
        stage("Compile"){
            steps{
                sh "mvn clean compile"
            }
        }
        
         stage("Test Cases"){
            steps{
                sh "mvn test"
            }
        }
        
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonarserver') {
                    sh ''' mvn sonar:sonar -Dsonar.projectName=Devops -Dsonar.java.binaries=. -Dsonar.projectKey=Devops '''
    
                }
            }
        }
        
         stage("Build"){
            steps{
                sh " mvn clean install"
            }
        }
    }
}
