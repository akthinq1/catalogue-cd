// Get verison from CI, place values in value.helm and deploy
// install kubectl in jenkis agent

pipeline{
    agent{
        label 'AGENT-1'
    }

    environment{

    }

    options{

    }

    parameters{

    }

    stages{
        stage(deploy){
            steps{
                script{
                    withAWS(credentials: 'aws-auth', region: 'us-east-1'){

                    }
                }
            }
        }
    }
}