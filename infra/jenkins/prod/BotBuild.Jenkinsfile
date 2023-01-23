pipeline {
    agent {
         docker {
            // TODO build & push your Jenkins agent image, place the URL here
            image '352708296901.dkr.ecr.eu-west-2.amazonaws.com/schiff-jenkins-new-agent:latest'
            args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'

        }

    }
    environment {
           REGISTRY_URL = "352708296901.dkr.ecr.eu-west-2.amazonaws.com"
           IMAGE_TAG = "0.0.$BUILD_NUMBER"
           IMAGE_NAME = "schiff-botbuild-prod"

    }
    stages {
        stage('Build') {
            steps {
                // TODO dev bot build stage
                sh '''
                echo "building ...""
                sudo aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin 352708296901.dkr.ecr.eu-west-2.amazonaws.com
                sudo docker build -t $IMAGE_NAME:$IMAGE_TAG . -f services/bot/Dockerfile
                sudo docker tag $IMAGE_NAME:$IMAGE_TAG $REGISTRY_URL/$IMAGE_NAME:$IMAGE_TAG
                sudo docker push $REGISTRY_URL/$IMAGE_NAME:$IMAGE_TAG
                echo "done"
                '''
            }
        }

        stage('Trigger Deploy') {
            steps {
                build job: 'BotDeploy', wait: false, parameters: [
                    string(name: 'BOT_IMAGE_NAME',value:"${REGISTRY_URL}/${IMAGE_NAME}:${IMAGE_TAG}")
                ]
            }
        }
    }
}