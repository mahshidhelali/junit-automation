pipeline {

    agent any
    stages {

        stage('Checkout Codebase'){
            steps{
                cleanWs()
                checkout scm: [$class: 'GitSCM', branches: [[name: '*/main']],userRemoteConfigs:
                [[url: 'https://github.com/mahshidhelali/junit-automation.git']]]
            }
        }

        stage('Build'){
            steps{
                bat """
                md lib
                cd C://ProgramData//Jenkins//.jenkins//workspace//JunitAutomation//src 
                javac -cp "C://Users//mahshidhelalimo//Downloads//junit-automation-main//junit-automation-main//lib//junit-platform-console-standalone-1.7.0-all.jar" CarTest.java Car.java App.java
                """
            }
        }

        stage('Test'){
            steps{
                bat "cd C://ProgramData//Jenkins//.jenkins//workspace//JunitAutomation//src"
                bat "java -jar C://Users//mahshidhelalimo//Downloads//junit-automation-main//junit-automation-main//lib//junit-platform-console-standalone-1.7.0-all.jar -cp "." --select-class CarTest --reports-dir='reports'"
                junit 'src/reports/*-jupiter.xml'
            }
        }

        stage('Deploy'){
            steps{
                sh 'cd src/ ; java App' 
            }
        }
    }

}
