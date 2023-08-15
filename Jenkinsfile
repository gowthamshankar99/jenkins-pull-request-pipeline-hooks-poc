pipeline {
    agent any
    stages {        
        stage('Validate CF Templates') {
            steps {
                script {
                    def skipSteps = false
                    echo "****************"
                    //print("$IF_MERGED")
                    def jsonObject = new groovy.json.JsonSlurper().parseText("$IF_MERGED")
                    //print(jsonObject)
                    def action = new groovy.json.JsonSlurper().parseText(jsonObject.payload[0]).action
                    
                    println "Action: $action    "
                    if(action == "synchronize") {
                        echo "Condition was met. Exiting the pipeline successfully."
                        skipSteps = true
                        return                    
                    }
                    def templatesDir = ''  // assuming this is where the repo is cloned test addsss

                    // List all CloudFormation template files in the directory
                    //def templateFiles = findFiles(glob: '**/*.json')

                    // Loop through each template file and validate
                    //for (def templateFile in templateFiles) {
                    //    def templatePath = templateFile.path
                    //    echo "Validating template: ${templatePath}"

                        // Execute the AWS CLI command to validate the template
                    //    sh "aws cloudformation validate-template --template-body file://${templatePath}"
                    // }
                }
            }
        }
        stage('cfn-nag cfn templates') {
            when {
                expression {
                    return skipSteps
                }
            }            
            steps {
                // Run your build and test commands here
                echo "cfn-nag the templates"
            }
        }        
    }
}
