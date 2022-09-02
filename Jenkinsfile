#!groovy
import org.jenkinsci.plugins.pipeline.modeldefinition.Utils

boolean validate = true
boolean test = false

def MY_REPO = "cfn-guard"
def ORG_NAME = "etapemejame"

def ENVIRONMENTS = [
    "sandbox": [
        "label": "blek_sandbox_account",
        "validate": true,
        "test": false
    ],
    "dev": [
        "label": "blek_dev_account",
        "validate": true,
        "test": false
    ],
    "prod": [
        "label": "blek_prod_account",
        "validate": false,
        "test": false
    ]
]

def FILE_TO_UPLOAD = "./cfn_templates/os_domain.yaml"
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
        stage('Validate-Templates')
        {
            steps
            {
                script 
                {   
                    sh "docker pull etapeblek/cfn-guard:v2.0.4"
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
                                withAWS(region:'us-west-2',credentials:'aws'){
                                    sh 'echo "Uploading content with AWS creds"'
                                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: "${file.path}", bucket: "blek-jenkins-upload-us-west-2")
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}