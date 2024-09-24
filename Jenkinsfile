pipeline {
    agent { label "master" }
    tools {
        maven 'maven'
    }
    environment {
        IMAGE = "springboot_jenkins"
    }
    stages {

        stage("build") {
            steps {
              sh ' mvn clean install '
              sh ' docker build -t ${IMAGE}:${BUILD_NUMBER} . '
            }
        }

        stage("test") {
            steps {
                echo "testing the application"
            }
        }

       
        
    }
}
