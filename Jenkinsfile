pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes cluster') {
            steps {
             withKubeCredentials(kubectlCredentials: [[
    credentialsId: 'k8token',
    serverUrl: 'https://0579D5551F40F49ADE90EA1E6E685767.gr7.us-east-1.eks.amazonaws.com',
    namespace: 'webapps'
]]) {
                    sh "kubectl apply -f deployment-service.yml"
                    sleep 60
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8token', namespace: 'webapps', serverUrl: 'https://0579D5551F40F49ADE90EA1E6E685767.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
