pipeline {
    agent any
    stages{
        stage("checkout"){
            steps{
                git url:"https://github.com/ghanatava/thedevopsproject.git", branch:"main"
            }
        }
        stage("build"){
            environment{
                DOCKERHUB = credentials("DOCKERHUB")
            }
            steps{
                sh "docker build ./frontend -t $DOCKERHUB_USR/auth-frontend"
                sh "docker build ./backend -t $DOCKERHUB_USR/auth-backend"
                sh "docker build ./nginx -t $DOCKERHUB_USR/auth-nginx"
            }
        }
        stage("push"){
            environment{
                DOCKERHUB = credentials("DOCKERHUB")
            }
            steps{
                sh '''
                    docker login -u $DOCKERHUB_USR -p $DOCKERHUB_PSW
                    docker push $DOCKERHUB_USR/auth-frontend
                    docker push $DOCKERHUB_USR/auth-backend
                    docker push $DOCKERHUB_USR/auth-nginx
                '''
            }
        }
    }
}