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
                publishHTML (target: [
                    reportDir: 'build/reports/jacoco/test/html', 
                    reportFiles: 'index.html', 
                    reportName: "JaCoCo Report"
                ])
            }
        }
        stage('Static Code Analysis'){
            steps{
                sh './gradlew checkstyleMain'
                publishHTML (target: [
                    reportDir: 'build/reports/checkstyle/', 
                    reportFiles: 'main.html', 
                    reportName: "Checkstyle Report"
                ])
            }
        }
        stage('SonarQube Code Quality Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "./gradlew sonarqube"
                }
            }
        }
        stage("SonarQube Quality Gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
    }
}