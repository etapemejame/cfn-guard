#!groovy
import org.jenkinci.plugins.pipeline.modeldefinition.Utils

// Pipeline starts here
pipeline {
    agent { label 'linux' }
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
                {   checkout scm
                    echo "Hello World. This is a test Jenkins Pipeline"
                    sh "sudo yum update"
                    sh "sudo yum install curl -y"
                    sh "curl https://sh.rustup.rs -sSf | sh -s -- -y"
                    sh "curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/aws-cloudformation/cloudformation-guard/main/install-guard.sh | sh"
                    sh "sudo cp ~/.guard/bin/cfn-guard /usr/local/bin"
                    echo "PATH=$PATH:~/.guard/bin/"
                    sh "cfn-guard --version"
                    sh "cfn-guard validate -r rule.guard -d os_domain.yaml"
                }
            }
        }
    }
}