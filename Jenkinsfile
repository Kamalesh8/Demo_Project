pipeline {
    agent "docker-slave"

    stages {
        
        stage ("Build") {
            steps {
                sh "mvn clean install -f MyWebApp/pom.xml"
            }
        }
        
        // stage ("Code scan") {
        //     steps {
        //      withSonarQubeEnv("My_SonarQube") {
        //         sh "mvn sonar:sonar -f MyWebApp/pom.xml"
        //      }   
        //     }
        // }     
        
    }
}
