/*
    Note:
    
    Windows users use "bat" instead of "sh"
    For ex: bat 'docker build -t=vinsdocker/selenium .'
    
    Do not use "vinsdocker" to push. Use your dockerhub account
*/
pipeline{

    agent any

    stages{

        stage('Build Jar'){
            steps{
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Build Image'){
            steps{
                bat 'docker build -t=dockerizedalpay/selenyumwithalpay .'
            }
        }

        stage('Push Image'){
            environment{
                // assuming you have stored the credentials with this name
                DOCKER_HUB = credentials('dockerhub-creds')
            }
            steps{
                // There might be a warning.
                bat 'docker login -u %DOCKER_HUB_USR% -p %DOCKER_HUB_PSW%'
                bat 'docker push dockerizedalpay/selenyumwithalpay'
            }
        }

    }

    post {
        always {
            bat 'docker logout'
        }
    }

}