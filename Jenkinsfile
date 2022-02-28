@Library(['github.com/indigo-dc/jenkins-pipeline-library@release/2.1.0']) _

def projectConfig

pipeline {
    agent any

    stages {
        stage('OpenAPI linter') {
            steps {
                script {
                    projectConfig = pipelineConfig(
                        configFile: './.sqa/config_style.yml',
                        scmConfigs: [ localBranch: true ]
                    )
                    buildStages(projectConfig)
                }
            }
            post {
                cleanup {
                    cleanWs()
                }
            }
        }
        stage('SQA baseline dynamic stages') {
            when {
                anyOf {
                    branch 'staging'
                }
            }
            steps {
                script {
                    projectConfig = pipelineConfig(
                        configFile: './.sqa/config_docs.yml',
                        scmConfigs: [ localBranch: true ]
                    )
                    buildStages(projectConfig)
                }
            }
            post {
                cleanup {
                    cleanWs()
                }
            }
        }
    }
}
