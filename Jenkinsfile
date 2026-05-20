pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes cluster') {
            steps {
             withKubeCredentials(kubectlCredentials: [[
    credentialsId: 'k8-token',
    serverUrl: 'https://90AA9BE12F033DBB7FBD43552150D6C5.gr7.us-east-1.eks.amazonaws.com',
    namespace: 'webapps'
]]) {
                    sh "kubectl apply -f deployment-service.yml"
                    sleep 60
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://90AA9BE12F033DBB7FBD43552150D6C5.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
