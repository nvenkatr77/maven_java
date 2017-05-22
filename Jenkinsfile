pipeline {
  agent any
  stages {
    stage('Source Code') {
      steps {
        git 'https://github.com/nvenkatr77/mvnrepo.git'
      }
    }
    stage('mvn compile') {
      steps {
        parallel(
          "mvn compile": {
            sh 'mvn clean compile package'
            
          },
          "mvn nexus deploy": {
            sh 'mvn deploy'
            
          }
        )
      }
    }
    stage('Tomcat-Deploy') {
      steps {
        sh '''JNAME=$(echo $JOB_NAME |cut -d / -f2)





sudo su - javaee7 -c "/home/javaee7/deploy-pl.sh $JNAME"'''
      }
    }
  }
}