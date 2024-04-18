pipeline {
    agent any
    stages {
        stage ('Init') {
            steps {
                echo "Hello from an inline pipeline script"
                echo "Job name: ${env.JOB_NAME}"
                echo " Build ID: ${env.BUILD_ID}"
                echo "Node name: ${env.NODE_NAME}"
                echo "Workspace: ${env.WORKSPACE}"
            }
        }
        stage ('Set and read environment variable') {
            environment {DENV = 'test'}
            input {
                    message "Process to read DENV env variable ?"
                    ok "Proceeding"
            }
            steps {
                echo "Running in ${env.DENV}"
            }
        }
        stage ('Create exception') {
            steps {
                script {
                    env.EXC = input message: 'Trigger an exception ?', ok: 'Continue',
                            parameters: [choice(name: 'EXC', choices: 'yes\nno', description: 'Trigger an exception ?')]
                    if (env.EXC == 'yes') {def trigger_exc = 10/0}   
                }
            }
        }
    }
    post{
        success { echo "It was a success!"}
        failure { echo "You cannot divide by zero!"}        
    }
}


