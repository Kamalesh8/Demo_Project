pipeline {
    agent { label 'docker-slave' }
    parameters {
        booleanParam(name: 'skip_test', defaultValue: false, description: 'Set to true to skip the test stage')
    }
    stages {
        
        stage("Pull code") {
            steps { checkout scmGit(branches: [[name: '*/develop']], extensions: [], userRemoteConfigs: [[credentialsId: '276a167d-0358-4bc7-b196-ddf7cefeb4e1', url: 'https://github.com/Kamalesh8/Demo_Project.git']]) }
        }
        
        stage ("Build") {
            steps {
                sh "mvn clean install -f MyWebApp/pom.xml"
            }
        }
        
        stage ("Code Scan Main Branch") {
            when {
                branch 'main'
                expression { params.skip_test != false }
            }
            steps {
             echo "From Main Branch"   
             withSonarQubeEnv("sonarserver") {
                sh "mvn sonar:sonar -f MyWebApp/pom.xml"
             } 
            }           
        }
        stage ("Code Scan develop Branch") {

             when {
                branch 'develop'
                expression { params.skip_test != true }
            }
            steps {
            echo "From develop branch"
             withSonarQubeEnv("sonarserver") {
                sh "mvn sonar:sonar -f MyWebApp/pom.xml"
             } 
            }
        }
    }
}
