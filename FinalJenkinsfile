pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/akshu20791/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t akshu20791/myprojectnew:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push akshu20791/myprojectnew:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
                script{
                    sh 'sudo docker run -itd --name My-project-con -p 8089:80 akshu20791/myprojectnew:v1'
                       }
                    }
                }
    }
}
