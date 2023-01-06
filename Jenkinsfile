pipeline {
    agent any
    tools{
       maven "local_maven"
    }
    stages {
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
           steps{
               sh "mvn clean package"
           }
           post{
               success{
                   echo "Archiving the Artifacts"
                   archiveArtifacts artifacts: '**/target/*.war'
               }
           }
        }
        stage('Deploy to tomcat') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'c3e73ff1-898f-4e93-8569-c4220fddf025', path: '', url: 'http://localhost:8081/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
