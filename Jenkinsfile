pipeline {
  agent any
  stages {
    stage('scm checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/LohadeDarshan/maven-project.git'
      }
    }

    stage('package job') //validate then compile and package
    {
      steps {
        withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'jenkins-maven', mavenSettingsConfig: '', traceability: true) {
          sh 'mvn package'
        }
      }
    }

    stage('deploy job') //validate then compile and package
    {
      steps {
        sshagent(['deploy-to-tomcat']) {
          sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war root@192.168.253.143:usr/share/tomcat/webapps'
          }
        }
      }
    }
  }
