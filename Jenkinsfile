pipeline {
    agent { label 'docker-slave' }

    stages {
        
        stage("Pull code") {
            steps { checkout scmGit(branches: [[name: '*/develop']], extensions: [], userRemoteConfigs: [[credentialsId: '276a167d-0358-4bc7-b196-ddf7cefeb4e1', url: 'https://github.com/Kamalesh8/Demo_Project.git']]) }
        }
        
        stage ("Build") {
            steps {
                sh "mvn clean install -f MyWebApp/pom.xml"
            }
        }
        
        stage ("Code Scan Develop Branch") {
            when {
                branch 'develop'
            }
            steps {
             withSonarQubeEnv("sonarserver") {
                sh "mvn sonar:sonar -f MyWebApp/pom.xml"
             } 
            }
        }

        stage ("Code Scan main Branch") {
            when {
                branch 'main'
            }
            steps {
             withSonarQubeEnv("sonarserver") {
                sh "mvn sonar:sonar -f MyWebApp/pom.xml"
             } 
            }
        }
    }
}
