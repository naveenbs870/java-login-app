pipeline {
    agent any
    environment {
        PATH = "$PATH:/usr/share/maven-3.6.3/bin"
    }
    stages {
        stage('Clone') {
            steps {
                sh 'rm -rf hello-world-war'
                sh 'git clone https://github.com/naveenbs870/hello-world-war.git'
            }
        }
        stage('Build') {
            steps {
                dir('hello-world-war'){
                sh 'mvn clean package'
                }
            }
        }
        stage('Deploy step') {
             steps {
                 sh 'sudo cp ${WORKSPACE}/hello-world-war/target/hello-world-war-1.0.0.war /var/lib/tomcat9/webapps/'       
            }
        }
	stage('Test'){
            steps{
                sh 'mvn test'
            }
        }
		stage('SonarQube analysis') {
            steps{
                withSonarQubeEnv('sonarqube-8.3') { 
                sh ''' mvn verify sonar:sonar -Dsonar.login=admin -Dsonar.password=admin'''
                }
                
            }
        }
    }
}
