pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('pmd') {
            steps {
                bat 'mvn clean install'
                dir('docs-core') {
                    bat 'mvn clean install  -DskipTests'
                }
                dir('docs-web-common') {
                    bat 'mvn clean install'
                }
                dir('docs-web') {
                    bat 'mvn clean install'
                }

                bat 'mvn pmd:pmd'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}
