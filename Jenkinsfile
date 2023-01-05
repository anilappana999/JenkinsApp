pipeline {
    agent any
    tools{
       maven "local_maven"
    }
    stages {
//         stage('git repo & clean') {
//             steps {
//                 sh "rm -rf JenkinsApp1"
//                 sh "git clone https://github.com/Janakkapadiya/JenkinsApp1.git"
//                 sh "mvn clean -f JenkinsApp1"
//             }
//         }
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
               deploy adapters: [tomcat9(credentialsId: '9b8b4a74-8a22-4b9f-99eb-26157bd1cd3e', path: '', url: 'http://127.0.0.1:8080/')], contextPath: null, war: ''
            }
        }
    }
}
