pipeline {
    agent any
    stages {
        stage('build app') {
            steps {
               script {
                   echo "building the application..."
               }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "building the docker image..."
                }
            }
        }
        stage('deploy') {
            environment {
                AWS_ACCESS_KEY_ID = credentials('jenkins_aws_access_key_id')
                AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws_secret_access_key')
                AWS_DEFAULT_REGION = 'eu-west-2'
            }
            steps {
                script {
                   echo 'deploying docker image...'
                   sh '''
                       which aws || (apt-get update && apt-get install -y unzip curl && \
                       curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
                       unzip -o awscliv2.zip && ./aws/install)

                       aws eks update-kubeconfig --region eu-west-2 --name demo-cluster

                       kubectl create deployment nginx-deployment --image=nginx
                   '''
                }
            }
        }
    }
}