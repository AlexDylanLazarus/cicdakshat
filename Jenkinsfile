pipeline {
    agent any
    stages{
        stage('Build Maven'){
            steps{
                git url:'https://github.com/AlexDylanLazarus/cicdakshat/', branch: "master"
               sh 'mvn clean install'
            }
        }
        stage('packaging'){
	        steps{
	            sh 'mvn package'
	        }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t alexdylanlazarus/endtoendproject25may:v1 .'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push alexdylanlazarus/endtoendproject25may:v1'
                }
            }
        }
        
        
     stage('Deploy') {
            steps {
               script {
			sh 'docker run -dt --name My-first-containe22161 -p 8085:8080 9julysanlam:v1'
                    }
                }
            }
        }
    }
}
