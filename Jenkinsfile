pipeline {
    agent any
    
    triggers {
        // This ensures the pipeline is triggered by the GitHub webhook
        githubPush()
    }

    stages {
        stage('Build') {
            when {
                branch 'master' // Only run on master branch
            }
            steps {
                echo 'Building the master branch...'
                // Add your build steps here
            }
        }

        stage('Test') {
            when {
                branch 'master'
            }
            steps {
                echo 'Running tests for master branch...'
                // Add your test steps here
            }
        }

        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying the master branch...'
                // Add your deployment steps here
            }
        }
    }
}
