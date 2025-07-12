pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK 17' 
    }

    environment {
        SONARQUBE = 'My SonarQube Server'
    }

    stages {
        stage('Clone Repository') {
            steps {
                bat 'git clone https://github.com/syedmizba/maven-simple.git'
                dir('jen-sonar') {
                    bat 'dir'
                }
            }
        }

        stage('Build') {
            steps {
                dir('maven-simple') {
                    bat 'mvn clean install'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('maven-simple') {
                    withSonarQubeEnv("${SONARQUBE}") {
                        bat 'mvn sonar:sonar'
                    }
                }
            }
        }
    }
}
