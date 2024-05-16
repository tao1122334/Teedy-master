pipeline {
    agent any

    //  environment {
    //     KUBECONFIG = '/var/lib/jenkins/.kube/config'
    //     KUBERNETES_TOKEN = credentials('kubernetes-token')
    // }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }

         stage('k8s'){
            steps {
                script {
                    // 启动 Minikube
                    // bat ' minikube image load tlz970370568/teedy2024_manual:latest'
                    sh 'mkdir %USERPROFILE%\\.kube'
                    sh 'copy C:\\etc\\kubernetes\\kubelet.conf %USERPROFILE%\\.kube\\config'
                    sh 'kubectl expose deployment hello-node --type=LoadBalancer --port=8080'
                    sh 'minikube service hello-node'
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
    

