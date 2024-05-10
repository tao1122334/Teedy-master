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
                // 假设你有多个子模块，分别在 submod1, submod2 文件夹中
                dir('docs-core') {
                    bat 'mvn install -DskipTests'
                }
                dir('docs-web-common') {
                    bat 'mvn install -DskipTests'
                }
                dir('docs-web') {
                    bat 'mvn install -DskipTests'
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
