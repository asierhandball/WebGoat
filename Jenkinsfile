oipeline {
    agent any
    stages {
        stage('CI Phase') {
            steps {
                build 'Docker_Image_Control2'
                dependencyCheck additionalArguments: '', odcInstallation: 'D-C'
                
            }
        }
        stage('CD_Phase') {
            steps {
                build 'K8s_Deploying'
            }
        }
    }
    post {
        always {
            recordIssues enabledForFailure: true, tool: mavenConsole(), referenceJobName: 'Docker_Image_Control'
            recordIssues enabledForFailure: true, tools: [java(), javaDoc()], sourceCodeEncoding: 'UTF-8', referenceJobName: 'Docker_Image_Control'
            recordIssues enabledForFailure: true, tool: checkStyle(), sourceCodeEncoding: 'UTF-8', referenceJobName: 'Docker_Image_Control'
            recordIssues enabledForFailure: true, tool: cpd(), sourceCodeEncoding: 'UTF-8', referenceJobName: 'Docker_Image_Control'
            recordIssues enabledForFailure: true, tool: pmdParser(), sourceCodeEncoding: 'UTF-8', referenceJobName: 'Docker_Image_Control'
            recordIssues enabledForFailure: true, tool: spotBugs(), sourceCodeEncoding: 'UTF-8', referenceJobName: 'Docker_Image_Control'
            recordIssues enabledForFailure: true, tool: taskScanner(includePattern:'**/*.java', excludePattern:'target/**/*', highTags:'FIXME', normalTags:'TODO'), sourceCodeEncoding: 'UTF-8', referenceJobName: 'Docker_Image_Control'
            dependencyCheckPublisher pattern: ''
        }
    }
}
