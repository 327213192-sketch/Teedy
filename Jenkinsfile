pipeline {
    agent any

    tools {
        maven 'Maven'   // 必须和你全局工具配置里的名字完全一致
        jdk 'JDK11'    // 你也要在全局工具里配一个 JDK，名字叫 JDK11
    }

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
                    junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('生成JavaDoc') {
            steps {
                sh 'mvn javadoc:javadoc'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar, target/site/**', fingerprint: true
        }
    }
}
