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
              // sh ' mvn clean install '
              sh 'groups'
              // sh ' docker build -t ${IMAGE}:${BUILD_NUMBER} . '
            }
        }

        stage("test") {
            steps {
                echo "testing the application"
            }
        }

        stage("deploy") {
            steps {
                sh 'docker start springboot_jenkins || docker run --name springboot_jenkins -d -p 8081:8080 springboot_jenkins '
                sh ' docker ps '
            }
        }
        
    }
}
