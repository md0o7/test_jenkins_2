properties([pipelineTriggers([githubPush()])])

pipeline {
  agent any
  
 environment {
        LAST_SUCCESSFUL_BUILD = 0
    }
  
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
                    sh "cp warfile.war backup_warfile.war"
                    //sh "md@localhost take_backup.sh"
                    sh "jar -cvf warfile.war index.html"
                    echo 'Build successfully'
                }
            }
        }
      
        
        stage('Stage 3: Deploy code on Tomcat ') {
            steps {
                      echo "deploying... $BUILD_NUMBER $LAST_SUCCESSFUL_BUILD"
                    
                    //deploy adapters: [tomcat9(credentialsId: 'cd44540a-3e33-4775-996b-11eeb4df4099', path: '', url: 'http://localhost:8082/')], contextPath: 'tomcat_2', war: '**/warfile.war'
//                    deploy adapters: [tomcat9(credentialsId: 'cd44540a-3e33-4775-996b-11eeb4df4099', path: '', url: 'http://localhost:8082/')], contextPath: 'tomcat_backup', war: '**/backup_warfile.war'
            }
        }
      
      
        /*stage('Stage 4: Stop Start Tomcat Process') {
            steps {
                    //sh "md@localhost shutdown.sh startup.sh"
              script{
                sh "/Library/Tomcat9/bin/shutdown.sh"
                sh "/Library/Tomcat9/bin/startup.sh"
              }
                  
            }
         
        }*/
        
    }
        
        post {
          always {
            echo 'Post Build Actions:'
          }
          
          success {
            echo 'Build is Successful. Deploying New Build...'
            deploy adapters: [tomcat9(credentialsId: 'cd44540a-3e33-4775-996b-11eeb4df4099', path: '', url: 'http://localhost:8082/')], contextPath: 'tomcat_2', war: '**/warfile.war'
            deploy adapters: [tomcat9(credentialsId: 'cd44540a-3e33-4775-996b-11eeb4df4099', path: '', url: 'http://localhost:8082/')], contextPath: 'tomcat_backup', war: '**/backup_warfile.war'

          }
          
          unstable {
              echo 'unstable'
          }
          
          failure {
            //mail to: mail@gmail.com, subject: 'The Pipeline failed :('
            
            script {
                    echo 'build failed'
                    //build_id="localhost:8080/job/Trial2/lastSuccessfulBuild/buildNumber"
                    //echo "Last Successful Build : $build_id"
                    sh "cp backup_warfile.war  warfile.war"
                    
                }
          }
        }
        
        
      
      
    
}
