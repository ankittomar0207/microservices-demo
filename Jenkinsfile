https://github.com/ankittomar0207/microservices-demo.git



pipeline {
    agent master
    
    
    stages {
        stage('Git Checkout') {
            steps {
               git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/ankittomar0207/microservices-demo.git'
            }
        }
        stage('Deploy To Kubernetes') {
            steps {
               withKubeConfig(caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'k8-cred-25', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://10.67.190.25:6443') {
                        sh "kubectl apply -f ./release/kubernetes-manifests.yaml"
                }
            }
        }
        
        stage('Verify the Deployment') {
            steps {
               withKubeConfig(caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'k8-cred-25', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://10.67.190.25:6443') {
                        sh "kubectl get pods -n webapps"
                        sh "kubectl get svc -n webapps"
                }
            }
        }
        
        
    }
}
    
