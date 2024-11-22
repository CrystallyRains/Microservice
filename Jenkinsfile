pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withCredentials([string(credentialsId: 'k8-token', variable: 'TOKEN')]) {
                    sh """
                    kubectl apply -f deployment-service.yml --token=${env.TOKEN} --namespace=webapps
                    """
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                withCredentials([string(credentialsId: 'k8-token', variable: 'TOKEN')]) {
                    sh """
                    kubectl get svc --token=${env.TOKEN} --namespace=webapps
                    """
                }
            }
        }
    }
}
