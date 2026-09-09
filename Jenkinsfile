pipeline {
    agent any

    stages {
        stage('Pull Public Repo') {
            steps {
                echo 'Pulling the website files from public GitHub repository...'
                // Clean the workspace before pulling new files
                cleanWs()
                // No credentialsId needed because your repository is public
                git branch: 'main', url: 'https://github.com'
            }
        }

        stage('Deploy to Web Server') {
            steps {
                echo 'Cleaning target directory and deploying new website files...'
                // Clear old code from the Nginx directory
                sh 'sudo rm -rf /var/www/html/*'
                // Copy new files explicitly from Jenkins workspace to Nginx folder
                sh 'sudo cp -R ./. /var/www/html/'
            }
        }

        stage('Reload Nginx') {
            steps {
                echo 'Testing Nginx configuration and reloading service...'
                sh 'sudo nginx -t'
                sh 'sudo systemctl reload nginx'
            }
        }
    }
}
