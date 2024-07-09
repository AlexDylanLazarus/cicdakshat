pipeline {
    agent any
    stages{
        stage('Build Maven'){
            steps{
                git url:'https://github.com/AlexDylanLazarus/cicdakshat/', branch: "master"
               sh 'mvn clean install'
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
                   def dockerrm = 'sudo docker rm -f My-first-containe221 || true'
                    def dockerCmd = 'sudo docker run -dt --name My-first-containe2211 -p 8083:80 alexdylanlazarus/endtoendproject25may:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 alexdylanlazarus/endtoendproject25may:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.37.165 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.37.165 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
