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
                sh label: '', script: '''
                javac HelloWorld.java
                java HelloWorld
                '''
            }
        }

    }
    post{
        always{
            echo "========always========"
            script{
                def changelogString = gitChangelog returnType: 'STRING',
                                // from: [type: 'COMMIT', value: ''],
                                to: [type: 'REF', value: 'master'],
                                template: """
                                <h1> Git Changelog changelog </h1>

                                <p>
                                Changelog of Git Changelog.
                                </p>

                                {{#tags}}
                                <h2> {{name}} </h2>
                                {{#issues}}
                                {{#hasIssue}}
                                {{#hasLink}}
                                <h2> {{name}} <a href="{{link}}">{{issue}}</a> {{title}} </h2>
                                {{/hasLink}}
                                {{^hasLink}}
                                <h2> {{name}} {{issue}} {{title}} </h2>
                                {{/hasLink}}
                                {{/hasIssue}}
                                {{^hasIssue}}
                                <h2> {{name}} </h2>
                                {{/hasIssue}}


                                {{#commits}}
                                <p>
                                <h3>{{{messageTitle}}}</h3>

                                {{#messageBodyItems}}
                                <li> {{.}}</li> 
                                {{/messageBodyItems}}
                                </p>


                                {{/commits}}

                                {{/issues}}
                                {{/tags}}
                                """
                currentBuild.description = changelogString
            }
        }
    }
}
