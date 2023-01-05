pipeline {
    agent any
    stages {
        stage('git repo & clean') {
            steps {
                sh "rm -rf JenkinsApp1"
                sh "git clone https://github.com/Janakkapadiya/JenkinsApp1.git"
                sh "mvn clean -f JenkinsApp1"
            }
        }
        stage('install') {
            steps {
                sh "mvn install -f JenkinsApp1"
            }
        }
        stage('test') {
            steps {
                sh "mvn test -f JenkinsApp1"
            }
        }
        stage('build')
        {
           stages{
               sh "mvn clean package"
           }
           post{
               success{
                   echo "Archiving the Artifacts"
                   archiveArtifacts artifacts "**/target/*.war"
               }
           }
        }
        stage('Deploy to tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'c3e73ff1-898f-4e93-8569-c4220fddf025', path: '', url: 'http://127.0.0.1:8080/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
