pipeline {
 agent any
    stages {
        stage('Pull Code') {
            steps {
                // Pull code from GitHub repository
                git 'https://github.com/Deepika94/Project-Demo'
            }
        }

        stage('Grant Permissions') {
            steps {
                // Grant executable permissions to a file
                sh 'chmod +x build.sh'
                sh 'chmod +x deploy.sh'
            }
        }

        stage('Build') {
            steps {
                // Run build script
                sh './build.sh'
            }
        }

        stage('Docker Push') {
            steps {
                // Docker push based on branch name
                script {
                    if (env.GIT_BRANCH == 'origin/dev') {
                        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                        sh 'docker tag perumal007/react-apps:latest perumal007/dev:latest'
                        sh 'docker push perumal007/dev:latest'
                    } else if (env.GIT_BRANCH == 'origin/prod') {
                        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                        sh 'docker tag perumal007/react-apps:latest perumal007/prod:latest'
                        sh 'docker push perumal007/prod:latest'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                // Run deploy script
                sh './deploy.sh'
            }
        }
    }
}
