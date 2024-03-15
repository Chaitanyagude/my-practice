pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Chaitanyagude/my-practice.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Tomcat Deploy') {
            steps {
            sshagent(['tomcat']) {
                sh "scp -o StrictHostKeyChecking=no target/my-practice.war ec2-user@172.31.90.114:/opt/tomcat9/webapps/"
                sh "ssh ec2-user@172.31.90.114 /opt/tomcat9/bin/shutdown.sh"
                sh "ssh ec2-user@172.31.90.114 /opt/tomcat9/bin/startup.sh"
                }
            }
        }
    }
}
