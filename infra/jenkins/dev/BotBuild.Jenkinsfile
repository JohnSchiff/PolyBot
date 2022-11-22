pipeline {
    agent {
        docker {
            // TODO build & push your Jenkins agent image, place the URL here
            image '352708296901.dkr.ecr.eu-west-2.amazonaws.com/schiff-jenkins-ex1:1'
            args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
        
    }
    environment{
        REGISTRY_URL="352708296901.dkr.ecr.eu-west-2.amazonaws.com"
        IMAGE_NAME="schiff-repo"
    }
    stages {
        stage('Build') {
            when { changeset "common/*"}

            steps {
                // TODO dev bot build stage
                sh '''
                echo "building..."
                aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin $REGISTRY_URL     
                docker build -t $IMAGE_NAME:2 .
                docker tag $IMAGE_NAME:2 $REGISTRY_URL/$IMAGE_NAME:2
                docker push $REGISTRY_URL/$IMAGE_NAME:2

                '''
            }
        }

        stage('Trigger Deploy') {
            when { changeset "common/*"}

            steps {
                build job: 'BotDeploy', wait: false, parameters: [
                    string(name: 'BOT_IMAGE_NAME', value: "${REGISTRY_URL}/${IMAGE_NAME}:2")
                ]
            }
        }
    }
}