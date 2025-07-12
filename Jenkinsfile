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
                // Checking if the directory exists, if not then clone it
                script {
                    def repoDir = 'maven-simple'
                    if (!fileExists(repoDir)) {
                        bat "git clone https://github.com/syedmizba/maven-simple.git ${repoDir}"
                    }
                }
                dir('maven-simple') {
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
