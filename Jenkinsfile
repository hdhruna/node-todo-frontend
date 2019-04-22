try {
    node("master") {

    stage("Clone Node App") {
    git 'https://github.com/hdhruna/node-todo-frontend.git'
    currentBuild.result = 'SUCCESS'
    }
    stage("Build Node App") {
    sh "npm install"
    currentBuild.result = 'SUCCESS'
    }
    stage("Test Node App") {
    sh "npm test"
    currentBuild.result = 'SUCCESS'
    }
    }
} catch (Exception err) {
    currentBuild.result = 'FAILURE'
}
echo "Current build status : ${currentBuild.result}"
if (currentBuild.result == "FAILURE") {
    stage("Create Jira Bug") {
    def issue = [fields: [project: [key: 'TES'],
    summary: 'Build error',
    description: 'Build error',
    issuetype: [name: 'Bug']
    ]]
    def newIssue = jiraNewIssue issue: issue, site: 'Test Jira'
    echo newIssue.data.key
    }

} else {
    stage("Create Jira Task") {
    def issue = [fields: [project: [key: 'TES'],
    summary: 'Build successful',
    description: 'Build successful',
    issuetype: [name: 'Task']
    ]]
    def newIssue = jiraNewIssue issue: issue, site: 'Test Jira'
    echo newIssue.data.key
    }
}
