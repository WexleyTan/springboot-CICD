pipeline {
    agent { label "b" }
    tools {
        maven 'maven'
    }
    environment {
        IMAGE = "springboot_jenkins"
    }
    environment {
        IMAGE = "WexleyTan/springboot-CICD"
        DOCKER_IMAGE = "${IMAGE}:${BUILD_NUMBER}"
        DOCKER_CREDENTIALS_ID = 'neathtan'

        GIT_MANIFEST_REPO = "https://github.com/LynaSovann/springboot_manifest.git"
        GIT_BRANCH = "argocd"
        MANIFEST_REPO = "manifest-repo"
        MANIFEST_FILE_PATH = "manifests/deployment.yaml"
        GIT_CREDENTIALS_ID = 'https_access_token'
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
