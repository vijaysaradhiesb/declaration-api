pipeline {

    agent any

    options {
        timeout(time: 8, unit: 'HOURS')
        disableConcurrentBuilds()
    }

    triggers {
        gitlab(
            triggerOnPush: true,
            triggerOnMergeRequest: false,
            triggerOpenMergeRequestOnPush: 'never',
            acceptMergeRequestOnSuccess: false,
            triggerOnNoteRequest: false,
            branchFilterType: 'RegexBasedFilter',
            targetBranchRegex: 'feature/[0-9]{8}_[0-9]{4}_AE-[0-9]+_.*$',
            setBuildDescription: true,
            secretToken: 'xxxxx')
    }

    stages {
        stage('CleanUp') {
            steps {
                echo "CleanUp:: Cleaning Workspace"
                cleanWs()
            }
        }
        stage('Validate Trigger') {
            when {
                anyOf {
                    expression { env.gitlabSourceRepoURL == null }
                    expression { env.gitlabSourceBranch == null }
                }
            }
            steps {
                error("Error:: Repository and/or Branch:: NULL")
            }
        }
        stage('Deploy') {
            steps {
                script {
                    build job:'workflow-job',
                    parameters: [
                        [$class: 'StringParameterValue',    name: 'type', value: "seed"],
                        [$class: 'StringParameterValue',    name: 'branch', value: "${env.gitlabSourceBranch}"],
                        [$class: 'StringParameterValue',    name: 'username', value: "${gitlabUserName}".split(" ")[0].toLowerCase()],
                        [$class: 'StringParameterValue',    name: 'repository', value: "${env.gitlabSourceRepoURL}"]
                    ], wait: true, propagate : true
                }
            }
        }
    }
}
