pipeline {
    agent any
    stages {
        stage('Git Progress') {
            steps {
                git  branch: 'main', credentialsId: 'eub456', url: 'https://github.com/eub456/NginxTemplateForArgocd.git'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sshagent (credentials: ['argoCD']) {
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@3.34.127.63 argocd repo add https://github.com/eub456/NginxTemplateForArgocd.git"
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@3.34.127.63 argocd app create test --repo https://github.com/eub456/NginxTemplateForArgocd.git --sync-option ApplyOutOfSyncOnly=true --path templates --dest-server https://kubernetes.default.svc --dest-namespace default"
                    }
                }
            }
        }
    }
}
