pipeline {
    agent any

    environment {
        IMAGE_NAME = "dusqor815/myweb"
        IMAGE_TAG = ''
        registryCredential = 'docker-hub-dusqor815'
        dockerImage = ''
    }

    parameters {
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
        string(name: 'STAGE', defaultValue: 'PRD', description: 'Enter a stage')
    }
    stages {
        stage('Print parameters') {
            steps {
                echo "Stage: ${params.STAGE}"
            }
        }
        
        stage('docker-build') {
            steps {
                sh "pwd"
                
                // docker_image_tag = sh(returnStdout: true, script: 'date "+%Y%m%d_%H-%M-%S"').trim()
                // echo "${docker_image_tag}"
                
                // sh "sed -i 's/IMAGE_VERIOSN/${env.IMAGE_TAG}/g' Dockerfile"

                dockerImage = docker.build "${env.IMAGE_NAME}:latest"
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