pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // 拉取项目代码
                git branch: 'uinverse', url: 'https://github.com/upup-721/FizzBuzzEnterpriseEdition-4jenkins.git'
            }
        }

        stage('Build') {
            steps {
                // 执行 Maven 构建
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // 运行单元测试
                bat 'mvn test'
            }
            post {
                always {
                    // 发布 JUnit 测试结果
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                // 生成最终的构建包
                bat 'mvn package'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                // 这里可以添加实际的部署逻辑，例如部署到服务器
                echo 'Deploying to production...'
            }
        }
    }

    post {
        always {
            // 无论成功或失败，都会执行的步骤
            echo 'Pipeline finished.'
        }
    }
}
