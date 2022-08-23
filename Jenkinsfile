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
                    sh "sudo apt update"
                    sh "sudo apt install curl -y"
                    sh "sudo apt install build-essential -y"
                    sh "curl -o /tmp/sh.rustup.rs -sSf https://sh.rustup.rs && sh /tmp/sh.rustup.rs -y"
                    sh "curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/aws-cloudformation/cloudformation-guard/main/install-guard.sh | sh"
                    sh "sudo cp ~/.guard/bin/cfn-guard /usr/local/bin"
                    sh "export PATH=$PATH:~/.guard/bin/"
                    sh "cfn-guard --version"
                }
            }
        }
    }
}