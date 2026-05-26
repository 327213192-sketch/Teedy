pipeline {
    agent any
    stages {
        stage('Maven构建') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('PMD代码检查') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('运行单元测试') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('生成JavaDoc') {
            steps {
                sh 'mvn javadoc:jar'
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar, target/site/**/*', fingerprint: true
        }
    }
}
