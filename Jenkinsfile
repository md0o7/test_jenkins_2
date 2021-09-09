properties([pipelineTriggers([githubPush()])])

pipeline {
  agent any
  //tools{maven 'Maven'}
  /*  environment {
        JAVA_HOME = '/Library/Java/JavaVirtualMachines/openjdk-8.jdk/Contents/Home'
        MAVEN_HOME = '/usr/local/Cellar/maven'
        PATH = "${env.JAVA_HOME}/bin:${env.MAVEN_HOME}/bin:${env.PATH}"
    }*/
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
                    //sh "mvn clean install"
                    sh "jar -cvf warfile.war index.html"
                    echo 'Build successfully'
                }
            }
        }
      
        stage('Stage 3: Deploy code on Tomcat ') {
            steps {
                    //sh "ssh md@localhost Ip ./report_war_bkpup.sh"
                    //sh "scp jenkins workspace path for job user@serverip:/opt/tomcat-report/webapps/"
                    deploy adapters: [tomcat9(credentialsId: 'cd44540a-3e33-4775-996b-11eeb4df4099', path: '', url: 'http://localhost:8082/')], contextPath: 'tomcat_1', war: '**/*.war'
                  
            }
        }
      
        /*stage('Stage 4: Stop Start Tomcat Process') {
            steps {
                    sh "md@localhost shutdown.sh startup.sh"
                  
            }
         
        }*/
    }
}
