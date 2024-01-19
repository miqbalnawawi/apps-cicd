pipeline {
    agent any
    parameters {
        string(name: 'GIT_REPO_URL', defaultValue: 'https://github.com/miqbalnawawi/devops-automation.git', description: 'Git repository URL')
    }
    tools {
        maven 'maven_3_5_0'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout(['$class': 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: params.GIT_REPO_URL]]])
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
        stage('Push image to Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub-credential-id', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u miqbalnawawi -p '
                    }
                    sh 'docker push miqbalnawawi/devops-integration'
                }
            }
        }
    }
}
