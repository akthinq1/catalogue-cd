// Get verison from CI, place values in value.helm and deploy
// install kubectl in jenkis agent

pipeline{
    agent{
        label 'AGENT-1'
    }

    environment{
        appVersion = ""
        REGION = "us-east-1"
        ACC_ID = "741005748171"
        PROJECT = "roboshop"
        COMPONENT = "catalogue"
    }

    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }

    parameters{
        string(name: 'appVersion', description: 'Image version of the application')
        choice(name: 'deploy_to', choices: ['dev', 'qa', 'prod'], description: "pick the environment")
    }


    stages{
        stage('Deploy'){
            steps{
                script{
                    withAWS(credentials: 'aws-auth', region: 'us-east-1'){
                        sh """
                            aws eks update-kubeconfig --region $REGION --name "$PROJECT-${params.deploy_to}"

                            kubectl get nodes

                            kubectl apply -f 01-namespace.yml

                            // sed -i "s/IMAGE_VERSION/${params.appVersion}/g" values-${params.deploy_to}.yaml

                            // helm upgrade --install $COMPONENT -f values-${params.deploy_to}.yaml -n $PROJECT .

                        """
                    }
                }
            }
        }
    }
}

// helm need to pass values
// create namespce safely 
// namesapce will not create through pipline, but for practice we do here