pipeline {
    agent { label "b" }
    tools {
        maven 'maven'
    }
    environment {
        IMAGE = "neathtan/springboot-cd"
        DOCKER_IMAGE = "${IMAGE}:${BUILD_NUMBER}"
        DOCKER_CREDENTIALS_ID = 'neathtan'

        GIT_MANIFEST_REPO = "https://github.com/WexleyTan/springboot_manifest.git"
        GIT_BRANCH = "main"
        MANIFEST_REPO = "manifest-repo"
        MANIFEST_FILE_PATH = "deployment.yaml"
        GIT_CREDENTIALS_ID = 'wexleyaccess'
    }
    stages {

        stage("build") {
            steps {
              // sh ' mvn clean install '
              sh ' docker build -t ${IMAGE}:${BUILD_NUMBER} . '
            }
        }

    stage("push docker image") {
            steps {
                    echo "🚀 Pushing the image to Docker hub"
                    sh 'docker push ${DOCKER_IMAGE}'
                }
            }

        stage("test") {
            steps {
                echo "testing the application"
            }
        } 

        stage("Cloning the manifest file") {
            steps {
                sh "pwd"
                sh "ls -l"
                echo "🚀 Checking if the manifest repository exists and removing it if necessary..."
                sh '''
                    if [ -d "${MANIFEST_REPO}" ]; then
                        echo "🚀 ${MANIFEST_REPO} exists, removing it..."
                        rm -rf ${MANIFEST_REPO}
                    fi
                '''
                echo "🚀 Updating the image of the Manifest file..."
                sh "git clone -b ${GIT_BRANCH} ${GIT_MANIFEST_REPO} ${MANIFEST_REPO}"
                sh "ls -l"
            }
        }


        stage("Updating the manifest file") {
            steps {
                script {
                    echo "🚀 Update the image in the deployment manifest..."
                    sh """
                    sed -i 's|image: ${IMAGE}:.*|image: ${DOCKER_IMAGE}|' ${MANIFEST_REPO}/${MANIFEST_FILE_PATH}
                    """
                }
            }
        }

        stage("push changes to the manifest") {
            steps {
                script {
                    dir("${MANIFEST_REPO}") {
                        withCredentials([usernamePassword(credentialsId: GIT_CREDENTIALS_ID, passwordVariable: 'GIT_PASS', usernameVariable: 'GIT_USER')]) {
                            sh """
                            git -v
                            
                            """
                        }
                    }
                }
            }
        }

        
    }
}
