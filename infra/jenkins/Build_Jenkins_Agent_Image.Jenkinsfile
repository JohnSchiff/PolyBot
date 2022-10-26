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
            pwd
            cd /var/lib/jenkins/workspace/BotBuild/infra/jenkins
            echo Now  n her 
            pwd
            '''
        }
        }

        stage('Build Jenkins Agent Docker') {
            steps {
                sh'''
                cd /var/lib/jenkins/workspace/BotBuild/infra/jenkins
                docker build -t $IMAGE_NAME:$IMAGE_TAG -f JenkinsAgent.Dockerfile .
                docker tag $IMAGE_NAME:$IMAGE_TAG $REGISTRY_URL/$IMAGE_NAME:$IMAGE_TAG 
                docker push $REGISTRY_URL/$IMAGE_NAME:$IMAGE_TAG 
                 '''
                }
        }

    }
}