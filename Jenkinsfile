pipeline {
 agent any
 stages {
    stage('Prepare') {
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
                // 可以继续添加更多子模块
            }
        }
 stage('Build') { 
steps {
 bat 'mvn -B -DskipTests clean package' 
}
 }
 stage('pmd') {
 steps {
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