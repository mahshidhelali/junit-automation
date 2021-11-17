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
                MD lib
                cd lib 
                cd C://Program Files (x86)//GnuWin32//bin
                wget https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/1.7.0/junit-platform-console-standalone-1.7.0-all.jar'
                cd C://ProgramData//Jenkins//.jenkins//workspace//JunitAutomation//src 
                javac -cp "C://Users//mahshidhelalimo//Downloads//junit-automation-main//junit-automation-main//lib//junit-platform-console-standalone-1.7.0-all.jar" CarTest.java Car.java App.java
            """
            }
        }

        stage('Test'){
            steps{
                sh 'cd src/ ; java -jar ../lib/junit-platform-console-standalone-1.7.0-all.jar -cp "." --select-class CarTest --reports-dir="reports"'
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
