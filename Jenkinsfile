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
            steps{
                bat 'kubectl expose deployment hello-node --type=LoadBalancer --port=8080 --token=$KUBERNETES_TOKEN'
                bat ' minikube service hello-node'
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
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            // 归档Surefire报告
        archiveArtifacts artifacts: '**/target/custom-surefire-reports/**', fingerprint: true
        }
    }
}
