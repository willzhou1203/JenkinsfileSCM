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
            echo '''
                Project Name: $env.JOB_NAME
                Author: $env.CHANGE_AUTHOR
                Commit Info: $env.CHANGE_TITLE
                $currentBuild.description
            '''
            emailext body: '''Project Name: env.JOB_NAME
                    Author: env.CHANGE_AUTHOR
                    Commit Info: env.CHANGE_TITLE
                    currentBuild.description''', subject: '$DEFAULT_SUBJECT', to: '$DEFAULT_RECIPIENTS'
        }
    }
}
