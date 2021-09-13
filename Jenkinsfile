properties([pipelineTriggers([githubPush()])])

pipeline {
  agent any
    stages {
        stage('Stage 1: PULL code from Git') {
            steps {
               git branch: 'main', credentialsId: 'md0o7', url: 'https://github.com/md0o7/test_jenkins_2.git'
               echo 'Checkout code successfully'
            }
        }
        stage('Stage 2: Build Code') {
            steps {
                script {
                    //sh "cp warfile.war backup_warfile.war"
                    sh "md@localhost ./take_backup.sh"
                    sh "jar -cvf warfile.war index.html"
                    echo 'Build successfully'
                }
            }
        }
      
        stage('Stage 3: Deploy code on Tomcat ') {
            steps {
                    
                    deploy adapters: [tomcat9(credentialsId: 'cd44540a-3e33-4775-996b-11eeb4df4099', path: '', url: 'http://localhost:8082/')], contextPath: 'tomcat_2', war: '**/warfile.war'
                    deploy adapters: [tomcat9(credentialsId: 'cd44540a-3e33-4775-996b-11eeb4df4099', path: '', url: 'http://localhost:8082/')], contextPath: 'tomcat_backup', war: '**/backup_warfile.war'
            }
        }
      
        /*stage('Stage 4: Stop Start Tomcat Process') {
            steps {
                    sh "md@localhost shutdown.sh startup.sh"
                  
            }
         
        }*/
    }
}
