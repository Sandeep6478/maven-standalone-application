/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any

    environment {
        PATH = "/opt/maven3/bin:$PATH"
    }
    stages {
        stage('Git Checkout') {
            steps {
                git credentialsId: 'Jenkinsfile', url: 'https://github.com/Sandeep6478/maven-standalone-application.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
                sh 'mv target/*.war target/myweb.war'
            }
        }
        stage('deploy-dev') {
            steps {
                sshagent(['tomcat-new']) {
                    sh '''
                    scp -o StrictHostKeyChecking=no target/myweb.war  ec2-user@172.31.48.143:/home/ec2-user/apache-tomcat-9.0.73/webapps/

                    ssh ec2-user@172.31.48.143 /home/ec2-user/apache-tomcat-9.0.73/bin/shutdown.sh

                    ssh ec2-user@172.31.48.143 /home/ec2-user/apache-tomcat-9.0.73/bin/startup.sh

                '''
                }
            }
        }
    }
}
