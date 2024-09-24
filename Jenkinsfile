pipeline {
    agent { label "b" }
    tools {
        maven 'maven'
        jenkins 'jenkins'
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
