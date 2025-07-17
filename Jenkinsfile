pipeline {
    agent any
    stages {
        stage('scm checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/LohadeDarshan/maven-project.git'
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
        stage('build the code')
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn clean package'  // build the code
                }
            }
        }
        stage('create docker image') {
            steps {
                sh 'docker build -t myserverd/ethans954:latest .'
            }
        }
        stage('push docker image to dockerhub') {
            steps {
                withDockerRegistry(credentialsId: 'DockerHUBCred', url: 'https://index.docker.io/v1/') {
                    sh 'docker push myserverd/ethans954:latest'
                }
            }
        }
    }
}
