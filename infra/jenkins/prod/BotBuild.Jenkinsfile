pipeline {
    agent {
        docker {
            // TODO build & push your Jenkins agent image, place the URL here
            image '352708296901.dkr.ecr.eu-west-2.amazonaws.com/schiff-jenkins-ex1:107'
            args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

 // TODO prod bot build pipeline
}