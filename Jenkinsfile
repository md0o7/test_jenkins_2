properties([pipelineTriggers([githubPush()])])

pipeline {
  agent any
    environment {
        JAVA_HOME = '/usr/lib/jvm/jre-openjdk'
        MAVEN_HOME = '/opt/maven'
        PATH = "${env.JAVA_HOME}/bin:${env.MAVEN_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('Stage 1: PULL code from Git') {
            steps {
               git branch: 'Branch name', credentialsId: 'user', url: 'github repo'
               echo 'Checkout code successfully'
            }
        }
        stage('Stage 2: Build Code') {
            steps {
                script {
                    sh "mvn clean install"
                    echo 'Build successfully'
                }
            }
        }
        stage('Stage 3: Deploy code on Tomcat ') {
            steps {
                    sh "ssh user@server Ip ./report_war_bkpup.sh"
                    sh "jenkins workspace path for job user@serverip:/opt/tomcat-report/webapps/"
                  
            }
        }
        stage('Stage 4: Stop Start Tomcat Process') {
            steps {
                    sh "user@serverip stop_start_process_RP"
                  
            }
         
        }
    }
}