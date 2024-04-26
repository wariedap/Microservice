pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                script {
                    withKubeConfig(
                        credentialsId: 'k8s-token',
                        serverUrl: 'https://BEA53F9A5C2A9F84884C8FAF7D065CC7.gr7.us-east-1.eks.amazonaws.com',
                        clusterName: 'EKS-3',
                        namespace: 'webapps',
                        caCertificate: '',
                        contextName: '',
                        restrictKubeConfigAccess: false
                    ) {
                        sh "kubectl apply -f deployment-service.yml" // Deploying the YAML configuration
                        sleep 60 // Waiting for deployment to complete (adjust sleep time as needed)
                    }
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                script {
                    withKubeConfig(
                        credentialsId: 'k8s-token',
                        serverUrl: 'https://BEA53F9A5C2A9F84884C8FAF7D065CC7.gr7.us-east-1.eks.amazonaws.com',
                        clusterName: 'EKS-3',
                        namespace: 'webapps',
                        caCertificate: '',
                        contextName: '',
                        restrictKubeConfigAccess: false
                    ) {
                        sh "kubectl get svc -n webapps" // Verifying the deployed service
                    }
                }
            }
        }
    }
}
