pipeline {
    agent any

     environment {
        KUBECONFIG = '/var/lib/jenkins/.kube/config'
        KUBERNETES_TOKEN = credentials('kubernetes-token')
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }

         stage('k8s'){
            steps {
                script {
                    // 启动 Minikube
                    bat 'minikube start'

                    // 设置 kubectl 使用 Minikube 上下文
                    bat 'kubectl config use-context minikube'

                    // 确认 Minikube 和 Kubernetes 状态
                    bat 'minikube status'
                    bat 'kubectl get nodes'
                }
                }
            }
        }
        // stage('pmd') {
        //     steps {
        //         bat 'mvn clean install -DskipTests'
        //         bat 'mvn pmd:pmd'
        //     }
        // }
        // stage('Doc') {
        //     steps {
        //         bat 'mvn javadoc:jar'
        //     }
        // }
        // stage('Test Report') {
        //     steps {
        //         bat 'mvn test'
        //     }
        // }
    }
    
}
