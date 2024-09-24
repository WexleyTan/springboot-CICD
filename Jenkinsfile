pipeline {
    agent { label "b" }
    tools {
        maven 'maven'
    }
    environment {
        IMAGE = "neathtan/springboot-cd"
        DOCKER_IMAGE = "${IMAGE}:${BUILD_NUMBER}"
        DOCKER_CREDENTIALS_ID = 'neathtan'

        GIT_MANIFEST_REPO = "https://github.com/WexleyTan/springboot_manifest"
        GIT_BRANCH = "main"
        MANIFEST_REPO = "manifest-repo"
        MANIFEST_FILE_PATH = "deployment.yaml"
        GIT_CREDENTIALS_ID = 'personal_access_token'
    }
    stages {

        stage("build") {
            steps {
              sh ' mvn clean install '
              sh ' docker build -t ${IMAGE}:${BUILD_NUMBER} . '
            }
        }

    stage("push docker image") {
            steps {
                    echo "🚀 Pushing the image to Docker hub"
                    sh 'docker push ${DOCKER_IMAGE}'
                    
                }
            }
        }

        stage("test") {
            steps {
                echo "testing the application"
            }
        }

       
        
    }
}
