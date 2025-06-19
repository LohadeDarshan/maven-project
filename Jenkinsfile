pipeline {
  agent any
  stages {
    stage('scm checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/kumargaurav039/maven-project.git'
      }
    }

    stage('package job') //validate then compile and package
    {
      steps {
        withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
          sh 'mvn package'
        }
      }
    }

    stage('deploy job') //validate then compile and package
    {
      steps {
        sshagent(['deploy-to-tomcat']) {
          sh 'scp -o StrictHostKeyChecking=no webapp/target/ec2-user@172.31.13.100:usr/share/tomcat/webapps'
          }
        }
      }
    }
  }
}
