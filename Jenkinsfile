pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Iam-mithran/kuber.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t mohanimage /var/lib/jenkins/workspace/kuber'
                sh 'sudo docker tag nmohanimage iammithran/mohanimage:latest'
                sh 'sudo docker tag mohanimage iammithran/nmohanimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push iammithran/mohanimage:latest'
                sh 'sudo docker image push iammithran/nmohanimage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'kubectl apply -f /var/lib/jenkins/workspace/kuber/pod.yaml'
                sh 'kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}

