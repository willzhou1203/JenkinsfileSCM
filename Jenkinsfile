pipeline{
    agent any

    stages{
        stage("access to git") {
            steps {
                git credentialsId: 'b34bd2a4-65b1-4919-8354-b7e94b9b1da6', url: 'https://github.com/willzhou1203/Jenkins.git'
            }
        }

        stage("build") {
            steps {
                sh label: '', script: '''javac HelloWorld.java
                                         java HelloWorld'''
            }
        }

    }
    post{
        always{
            echo "========always========"
            sh label: '', script: 'git log -1'
            
            echo env.BUILD_NUMBER
        }
    }
}
