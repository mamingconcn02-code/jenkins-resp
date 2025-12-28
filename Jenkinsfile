pipeline {
    agent any

    environment {
        JAR_DIR = 'D:\\jenkins-deploy\\demo'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Change to demo1 directory') {
            steps {
                script {
                    // 切换到 demo1 目录
                    bat 'cd demo1'
                }
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Copy JAR') {
            steps {
                bat """
                    if not exist "${JAR_DIR}" mkdir "${JAR_DIR}"
                    copy /Y "demo1\\target\\*.jar" "${JAR_DIR}\\app.jar"
                """
            }
        }

        stage('Run JAR') {
            steps {
                bat """
                    start \"SpringBoot App\" java -jar "${JAR_DIR}\\app.jar"
                """
            }
        }
    }
}
