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
                    // bat ' minikube image load tlz970370568/teedy2024_manual:latest'
                    bat 'mkdir ~/.kube'
                    bat 'cp /etc/kubernetes/kubelet.conf  ~/.kube/config'
                    bat 'kubectl expose deployment hello-node --type=LoadBalancer --port=8080'
                    bat 'minikube service hello-node'
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
    

