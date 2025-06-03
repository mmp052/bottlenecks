pipeline {
    agent any
    environment {
        SERVICE = 'bottleneck'
        NAME = "mmp052/${env.SERVICE}"
    }
    stages {
        stage('Deploy grafana to Kubernetes') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {
                    sh '''
                        aws eks update-kubeconfig --name eks-store --region us-east-2
                        kubectl apply -f grafana/k8s/k8s.yaml
                    '''
                }
            }
        }

        stage('Deploy prometheus to Kubernetes') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {
                    sh '''
                        aws eks update-kubeconfig --name eks-store --region us-east-2
                        kubectl apply -f prometheus/k8s/k8s.yaml
                    '''
                }
            }
        }

        stage('Deploy redis to Kubernetes') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {
                    sh '''
                        aws eks update-kubeconfig --name eks-store --region us-east-2
                        kubectl apply -f redis/k8s/k8s.yaml
                    '''
                }
            }
        }
        
    }
}
