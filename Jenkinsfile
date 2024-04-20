pipeline {
    agent any

    environment {
        IMAGE_NAME = "dusqor815/myweb"
        registryCredential = 'docker-hub-dusqor815'
        dockerImage = ''
    }

    parameters {
        string(name: 'STAGE', defaultValue: 'PRD', description: 'Name of Stage')
        string(name: 'IMAGE_TAG', defaultValue: '', description: 'Tag of Docker image')
    }

    stages {
        stage('Print parameters') {
            steps {
                echo "Stage: ${params.STAGE}"
                echo "IMAGE_TAG: ${params.IMAGE_TAG}"
            }
        }
        
        stage('docker-build') {
            steps {
                echo 'Build Docker'
                script {
                    sh "pwd"
                    def docker_image_tag = params.IMAGE_TAG
                    if (docker_image_tag == ''){
                        docker_image_tag = sh(returnStdout: true, script: 'date -u "+%Y%m%d.%H.%M.%S.%Z"').trim()
                    }
                    sh "sed -i 's/IMAGE_VERIOSN/${docker_image_tag}/g' Dockerfile"
                    dockerImage = docker.build "${env.IMAGE_NAME}:${docker_image_tag}"
                }
            }
        }

        stage('docker-push'){
            steps{
                echo 'Push Docker'
                script {
                    docker.withRegistry('', registryCredential){
                        dockerImage.push()
                    }
                }
            }
        }
    }
}