// Pipeline starts here

pipeline {
    agent any
    options {
        timestamps()
    }
    stages 
    {
        stage('Hello')
        {
            steps
            {
                "sudo apt-get install curl -y"
                "sudo apt-get update; sudo apt install build-essential"
                sh '''
                echo Hello World. This is a test Jenkins Pipeline
                "curl -o sh.rustup.rs -sSf https://sh.rustup.rs && sh.rustup.rs -y"
                "cargo install cfn-guard"
                "cfn-guard --version"

                '''
            }
        }
    }
}