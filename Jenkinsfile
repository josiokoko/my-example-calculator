pipeline {
    agent any
    stages {
        stage('Compile') {
            steps{
                sh "./gradlew compileJava"
            }
        }
        stage('Unit Test'){
            steps{
                sh './gradlew test'
            }
        }
        stage('Code Coverage'){
            steps{
                sh './gradlew test jacocoTestCoverageVerification'
                sh './gradlew test jacocoTestReport'
                publishHTML (target: [reportDir: 'build/reports/jacoco/test/html', 
                                        reportFiles: 'index.html', reportName: "JaCoCo Report"
                ])
            }
        }
    }
}