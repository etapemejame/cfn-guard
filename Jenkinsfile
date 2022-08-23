// Pipeline starts here

pipeline {
    agent node
    options {
        timestamps()
    }
    stages 
    {
        stage('Hello')
        {
            steps
            {
                sh '''#!/bin/bash
                echo Hello World. This is a test Jenkins Pipeline
                "apt update; apt install curl -y"
                "apt install build-essential -y"
                "curl -o sh.rustup.rs -sSf https://sh.rustup.rs && sh.rustup.rs -y"
                "cargo install cfn-guard"
                "cfn-guard --version"

                '''
            }
        }
    }
}