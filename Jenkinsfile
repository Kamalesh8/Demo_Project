pipeline {
    agent { label 'docker-slave' }

    stages {
        
        stage("Pull code") {
            steps { checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '276a167d-0358-4bc7-b196-ddf7cefeb4e1', url: 'https://github.com/Kamalesh8/Demo_Project.git']]) }
        }
        
        stage ("Build") {
            steps {
                sh "mvn clean install -f MyWebApp/pom.xml"
            }
        }
        
        stage ("Code scan") {
            steps {
             withSonarQubeEnv("sonarserver") {
                sh "mvn sonar:sonar -f MyWebApp/pom.xml"
             } 
            }
        }
        
    }
}
