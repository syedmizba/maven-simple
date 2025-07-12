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
                // Use Jenkins' native git functionality to clone the repository
                git url: 'https://github.com/syedmizba/maven-simple.git', branch: 'main'
                dir('maven-simple') {  // Correct directory name after clone
                    bat 'dir'  // List the directory to verify the clone
                }
            }
        }

        stage('Build') {
            steps {
                dir('maven-simple') {
                    bat 'mvn clean install'  // Build the project
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('maven-simple') {
                    withSonarQubeEnv("${SONARQUBE}") {  // Run SonarQube analysis
                        bat 'mvn sonar:sonar'
                    }
                }
            }
        }
    }
}
