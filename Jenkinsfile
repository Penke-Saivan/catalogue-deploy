pipeline {
    // ------------pre-build-----------------

    // agent configured
    agent {
        node {
            label 'AGENT-1'
        }
    }

    // environment variables
    environment {
        COURSE = 'Jenkins'
        appVersion = ''
        ACC_ID = '131676642204'
        PROJECT = 'roboshop'
        COMPONENT = 'catalogue'
        REGION = 'us-east-1'
    }
    //  after the timeout abort the pipeline
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    parameters {
        string(name: 'appVersion', description:'which version')
        choice(name: 'DEPLOY_TO', choices: ['qa', 'dev', 'prod'], description: 'Pick something')
    }

    // ------------------- build stage -----------------------
    stages {
                stage('Deploy') {
            steps {
                script {
                    withAWS(region: 'us-east-1', credentials: 'aws-creds') {
                        sh """
                        ls -l
                        pwd

                        aws eks update-kubeconfig --name ${PROJECT}-${params.DEPLOY_TO} --region ${REGION}
                        kubectl get nodes
                        ls -l
                       """
                    }
                }
            }
                }
    }

        // --------------------------post build--------------------
        post {
        always {
            echo 'I will always say Hello again!'
            cleanWs()
        }
        success {
            echo 'Success---------------'
        }
        failure {
            echo 'failure---------------'
        }
        aborted {
            echo 'someone -aborted--------------------------------'
            echo 'may be timeeout  -aborted--------------------------------'
        }
        }
}
