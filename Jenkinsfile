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
                script 
                {
                    echo "Hello World. This is a test Jenkins Pipeline"
                    sh "sudo apt update; apt install curl -y"
                    sh "sudo apt install build-essential -y"
                    sh "curl -o sh.rustup.rs -sSf https://sh.rustup.rs && sh.rustup.rs -y"
                    sh "cargo install cfn-guard"
                    sh "cfn-guard --version"
                }
            }
        }
    }
}