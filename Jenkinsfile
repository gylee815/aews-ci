pipeline {
    agent any

    environment {
        IMAGE_NAME = "dusqor815/myweb"
        registryCredential = 'docker-hub-dusqor815'
        dockerImage = ''
    }

    parameters {
        string(name: 'STAGE', defaultValue: 'PRD', description: 'Name of Stage')
        string(name: 'IMAGE_TAG', defaultValue: 'latest', description: 'Tag of Docker image')
    }

    stages {
        stage('Print parameters') {
            steps {
                echo "Stage: ${params.STAGE}"
            }
        }
        
        stage('docker-build') {
            steps {
                echo 'Build Docker'
                script {
                    sh "pwd"
                    // current_time = sh(returnStdout: true, script: 'date -u "+%Y%m%d.%H.%M.%S.%Z"').trim()
                    // if (params.IMAGE_TAG == ''){

                    // }
                    IMAGE_TAG = sh(returnStdout: true, script: 'date -u "+%Y%m%d.%H.%M.%S.%Z"').trim()
                    sh "sed -i 's/IMAGE_VERIOSN/${params.IMAGE_TAG}/g' Dockerfile"
                    dockerImage = docker.build "${env.IMAGE_NAME}:${params.IMAGE_TAG}"
                }
                // docker_image_tag = sh(returnStdout: true, script: 'date "+%Y%m%d_%H-%M-%S"').trim()
                // echo "${docker_image_tag}"
                
                // sh "sed -i 's/IMAGE_VERIOSN/${env.IMAGE_TAG}/g' Dockerfile"

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