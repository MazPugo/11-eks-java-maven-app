#!/usr/bin/env groovy

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
            steps {
                script {
                   echo 'deploying docker image...'
                   withKubeConfig([credentialsId: 'lke-credentials', serverUrl: 'https://174a6357-86f0-4e61-921f-da8ace4b92ac.uk-lon-1-gw.linodelke.net:443']) {
                        sh 'kubectl create deployment nginx-deployment --image=nginx'
                   }
                }
            }
        }
    }
}
