pipeline{
    agent any
    tools
    {
        maven "maven"
    }
    stages{
        stage('checkout'){
            steps{
                git branch: 'master', url: 'https://github.com/velpularajeswari/WebApplication'
            }
        }
        stage('Package'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Imagre'){
            steps{
                sh "docker build -t rajeswari1994/maven-app:1.0.0 ."
            }
        }
        stage("push image"){
            steps{
                 withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerpwd')]) {
                 sh "docker login -u rajeswari1994 -p ${dockerpwd}"
                 sh "docker push rajeswari1994/maven-app:1.0.0"
            }
        }
        stage('Run Docker Container'){
            steps{
                sh "docker run -p 8081:8080 rajeswari1994/maven-app:1.0.0"
            }
        }
    }
}
}
