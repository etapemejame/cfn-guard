#!groovy
import org.jenkinci.plugins.pipeline.modeldefinition.Utils

// Pipeline starts here
pipeline {
    agent any
    options {
        timestamps()
    }
    node
    {
        stages 
        {
            stage('print-filename') {
                script {
                    def changedFiles = pullRequest.files.collect {
                            it.getFilename()
                        }
                        println "${changedFiles}"

                }
            }
            stage('Hello')
            {
                steps
                {
                    script 
                    {   checkout scm
                        echo "Hello World. This is a test Jenkins Pipeline"
                        sh "sudo yum update"
                        sh "sudo yum install curl -y"
                        sh "curl -o /tmp/sh.rustup.rs -sSf https://sh.rustup.rs && sh /tmp/sh.rustup.rs -y"
                        sh "curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/aws-cloudformation/cloudformation-guard/main/install-guard.sh | sh"
                        sh "sudo cp ~/.guard/bin/cfn-guard /usr/local/bin"
                        sh "export PATH=$PATH:~/.guard/bin/"
                        sh "cfn-guard --version"
                        sh "cfn-guard validate -r rule.guard -d os_domain.yaml"
                    }
                }
            }
        }
    }
}