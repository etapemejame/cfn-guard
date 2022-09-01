#!groovy

// Pipeline starts here
def MODIFIED_FILE = "payload.head_commit.modified"
echo "Recently modified file is ${MODIFIED_FILE}"
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
        stage('Validate-Templates')
        {
            steps
            {
                script 
                {   
                    sh "docker pull etapeblek/cfn-guard:v2.0.4"
                    // echo "Hello World. This is a test Jenkins Pipeline"
                    // sh "curl https://sh.rustup.rs -sSf | sh -s -- -y"
                    // sh "curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/aws-cloudformation/cloudformation-guard/main/install-guard.sh | sh"
                    // sh "sudo cp ~/.guard/bin/cfn-guard /usr/local/bin"
                    // echo "PATH=$PATH:~/.guard/bin/"
                    // sh "cfn-guard --version"
                    sh "docker run -i --mount type=bind,source=`pwd`/rules,target=/opt/rules --mount type=bind,source=`pwd`/cfn_templates,target=/opt/tests etapeblek/cfn-guard:v2.0.4 validate -r /opt/rules/rule.guard -d /opt/tests/os_domain.yaml"
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
                    // withAWS(region:'us-west-2',credentials:'aws'){
                    //     sh 'echo "Uploading content with AWS creds"'
                    //     s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: "`pwd`/cfn_templates/os_domain.yaml", bucket: "blek-jenkins-upload-us-west-2")
                    // }
                }
            }
        }
    }
}