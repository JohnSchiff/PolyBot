pipeline {
    agent any

    environment {
        REGISTRY_URL= "352708296901.dkr.ecr.eu-west-2.amazonaws.com"
        IMAGE_TAG= "$BUILD_NUMBER"
        IMAGE_NAME = "schiff-jenkins-ex1"
        REGION = "eu-west-2"
    }

    stages {
        stage('Echoing'){
        steps{
            sh '''
            sudo amazon-linux-extras enable docker
            sudo yum install amazon-ecr-credential-helper
            sudo -u jenkins mkdir -p /var/lib/jenkins/.docker
            echo '{"credsStore": "ecr-login"}' | sudo -u jenkins tee /var/lib/jenkins/.docker/config.json
            '''
        }
        }

        stage('Build Jenkins Agent Docker') {
            steps {
                sh'''
                // aws ecr get-login-password --region $REGION | docker login --username AWS --password-stdin $REGISTRY_URL
                 docker build -t $IMAGE_NAME:$IMAGE_TAG -f Build_Jenkins_Agent_Image.Jenkinsfile .
                 docker tag $IMAGE_NAME:$IMAGE_TAG $REGISTRY_URL/$IMAGE_NAME:$IMAGE_TAG 
                 
                 '''
                }
        }

    }
}