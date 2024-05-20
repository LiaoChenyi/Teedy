pipeline {
    agent any
    stages{
        stage('Package') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [],
                userRemoteConfigs: [[url: 'https://github.com/traccytian/Teedy_2024.git']])
                sh 'mvn -B -DskipTests clean package'
                }
            }
            // Building Docker images
            stage('Building image') {
                steps{
                //your command
                sh 'docker build -t teedy2024_manual .'
                }
            }
            // Uploading Docker images into Docker Hub
            stage('Upload image') {
                steps{
                //your command
                sh 'docker push seveneki/teedy:teedy2024_manual'
                }
            }
            //Running Docker container
            stage('Run containers'){
                steps{
                //your command
                sh 'docker run -d -p 8084:8080 --name teedy_manual01 teedy2024_manual'
                sh 'docker run -d -p 8082:8080 --name teedy_manual02 teedy2024_manual'
                sh 'docker run -d -p 8083:8080 --name teedy_manual03 teedy2024_manual'
                }
        }
    }
}