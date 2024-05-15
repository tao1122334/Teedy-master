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
                    bat 'minikube start --driver=docker --wait=all --extra-config=apiserver.enable-admission-plugins=NamespaceLifecycle --validate=false --wait-timeout=20m --v=9 --alsologtostderr --disable-driver-mounts'
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
    

