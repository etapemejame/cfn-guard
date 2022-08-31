#!groovy

// Pipeline starts here
pipeline {
    agent {label "linux"}
    options {
        timestamps()
    }
    stages 
    {
        stage('get-filename') {
            steps
            {
                script
                {
                    def changeLogSets = currentBuild.changeSets
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
            } 
        }
        stage('Hello')
        {
            steps
            {
                script 
                {   
                    echo "Hello World. This is a test Jenkins Pipeline"
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