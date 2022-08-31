#!groovy
import org.jenkinci.plugins.pipeline.modeldefinition.Utils

// Pipeline starts here

def base_branch = 'main'
pipeline {
    agent { local 'linux' }
    options {
        timestamps()
    }
    def changeLogSets = currentBuild.changeSets
    node
    {
        stages 
        {
            stage('print-filename') {
                script {
                    for (int i = 0; i < changeLogSets.size(); i++) {
                        def entries = changeLogSets[i].items
                        for (int j = 0; j < entries.length; j++) {
                            def entry = entries[j]
                            echo "${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}"
                            def files = new ArrayList(entry.affectedFiles)
                            for (int k = 0; k < files.size(); k++) {
                                def file = files[k]
                                echo "  ${file.editType.name} ${file.path}"
                            }
                        }
                    }
                }
                println "Base branch is ${base_branch}"
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