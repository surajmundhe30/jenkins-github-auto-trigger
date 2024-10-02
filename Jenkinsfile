pipeline {
    agent any
    triggers {
        // Optionally poll SCM to supplement GitHub webhook
        pollSCM('H/5 * * * *')
    }
    stages {
        stage('Build') {
            when {
                branch 'master'  // This ensures the pipeline only runs for master branch pushes
            }
            steps {
                echo 'Building master branch...'
                // Add your build steps here
            }
        }
    }
}
