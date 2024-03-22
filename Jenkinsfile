pipeline {
    agent any

     environment {
        PATH = "/opt/homebrew/bin:$PATH"
        AWS_EB_CREDENTIALS_ID = 'AWS_INFO'
        AWS_REGION = 'us-west-1'
        CLUSTER_NAME = 'multi-k8s'
    }

    stages {
        stage("Checkout") {
            steps {
                  git(
                  url: 'https://github.com/Dixit-Patel-1990/multi-kubernetes.git',
                  branch: "main"
                )
            }
        }

        stage('Deploy to Elastic Beanstalk') {
            steps {
                script {
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY', credentialsId: env.AWS_EB_CREDENTIALS_ID]]) {
                        sh '/opt/homebrew/bin/aws configure set aws_secret_access_key ${AWS_ACCESS_KEY_ID}'
                        sh '/opt/homebrew/bin/aws configure set aws_secret_access_key ${AWS_SECRET_ACCESS_KEY}'
                        sh '/opt/homebrew/bin/aws configure set region $AWS_REGION'
                        sh '/opt/homebrew/bin/aws eks update-kubeconfig --region $AWS_REGION  --name $CLUSTER_NAME'
                        sh '/opt/homebrew/bin/kubectl apply -f k8s'
                        sh '/opt/homebrew/bin/eksctl utils associate-iam-oidc-provider --cluster multi-k8s --approve'
                    }
                }
            }
        }
    }       
}
     
