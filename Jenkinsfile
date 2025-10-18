pipeline {
    agent any
    stages {
        stage('scm checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/LohadeDarshan/maven-project.git'
            }
        }
        stage('code validate') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn validate'   // validate the code
                }
            }
        }
        stage('code compile') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn compile'   // compile
                }
            }
        }
        stage('code test') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn test'   // test
                }
            }
        }
        stage('code build') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn package'   // validate + compile + test + package
                }
            }
        }
        stage('create docker image') {
            steps {
                sh 'docker build -t e31531469/ethans954:latest1 .'
            }
        }
        stage('push docker image to dockerhub') {
            steps {
                withDockerRegistry(credentialsId: 'DockerHubCredentials', url: 'https://index.docker.io/v1/') {
                    sh 'docker push e31531469/ethans954:latest'
                }
            }
        }
        stage('code deploy') { // will deploy on target machine
            steps {
                sshagent(['DevCICD']) {
                    sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war root@10.23.213.210:/var/lib/tomcat10/webapps'
                }
            }
        }
    }
}