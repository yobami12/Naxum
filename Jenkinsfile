pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/yobami12/Naxum.git'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Copy to Docker Volume') {
            steps {
                script {
                    def targetPath = '/var/lib/docker/volumes/v1_wp-data/_data'
                    sh """
                        echo 'Copying files to Docker volume...'
                        sudo cp -r * ${targetPath}/
                        echo 'Copy complete.'
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully.'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
