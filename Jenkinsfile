pipeline {
    agent any
    stages {        
        stage('Validate CF Templates') {
            steps {
                script {
                    def templatesDir = ''  // assuming this is where the repo is cloned test addss

                    // List all CloudFormation template files in the directory
                    def templateFiles = findFiles(glob: '**/*.json')

                    // Loop through each template file and validate
                    for (def templateFile in templateFiles) {
                        def templatePath = templateFile.path
                        echo "Validating template: ${templatePath}"

                        // Execute the AWS CLI command to validate the template
                        sh "aws cloudformation validate-template --template-body file://${templatePath}"
                    }
                }
            }
        }
        stage('cfn-nag cfn templates') {
            steps {
                // Run your build and test commands here
                echo "cfn-nag the templates"
            }
        }        
    }
}
