pipeline{
    agent { label 'dev' }
    
    stages {
        stage('Code'){
            steps {
                git url: 'https://github.com/Shubhgole/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build and Test'){
            steps {
                sh 'docker build . -t shubhgole/node-todo-app-cicd:latest'
            }
        }
        stage('Login and Push Image') {
    steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUsername')]) {
            sh "docker login -u ${dockerHubUsername} -p ${dockerHubPassword}"
            sh "docker push shubhgole/node-todo-app-cicd:latest"
        }
    }
}
        stage('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d --build web'
            }
        }
    }
}
