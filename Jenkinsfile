pipeline {
    
    triggers {
        githubPush() // Trigger the pipeline on GitHub push events
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git url: 'git@https://github.com/surajmundhe30/jenkins-github-auto-trigger.git', branch: 'master'
            }
        }
