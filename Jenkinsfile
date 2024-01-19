pipeline {
    agent any
    parameters {
        string(name: 'GIT_REPO_URL', defaultValue: , description: 'Git repository URL')
    }
    tools {
        maven 'maven_3_5_0'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout(['': 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: params.GIT_REPO_URL]]])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t miqbalnawawi/devops-integration .'
                }
            }
        }
        // Additional stages can be added here
    }
}
