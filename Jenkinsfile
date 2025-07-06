pipeline {
    agent any
    stages {
        stage('scm checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/LohadeDarshan/maven-project.git'
            }
        }

        stage('code validate') //validate then compile and package
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn validate'  // validate the code
                }
            }
        }
        stage('code compile') 
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn compile'  // compile
                }
            }
        }
        stage('code test')
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn test'  // test
                }
            }
        }
        stage('code build')
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn package'  // validate + compile + test + package 
                }
            }
        }

        stage('code deploy') 
        {
            steps{
                sshagent(['ClientCICD']) {
                    sh 'scp -o StrictHostKeyChecking=no /webapp/target/webapp.war root@192.168.253.143:/opt/tomcat/webapps'
                    }
  
            }


            }
        }
    }
