pipeline {
    agent any

    stages {
        stage('Git push') {
            steps {
                sh 'rm -rf *'
                sh 'git clone https://github.com/nithishvjs/Simple-flask-app.git'
            }
        }
        stage('Docker build') {
            steps {
                sh '''
                docker rmi flask-app || true
                docker build -t flask-app -f ./flask-app/Dockerfile flask-app
                '''
            }
        }
        stage('Docker Deploy') {
            steps {
                sh '''
                docker stop myapp || true
                docker rm myapp || true
                docker run -itd --name myapp -p "5000:5000" flask-app
                '''
            }
        }
    }
}
