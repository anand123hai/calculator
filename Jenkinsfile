pipeline {
    agent {label "anand-windows-jenkins-master"}
    stages {
            stage("Checkout") {
                steps {
                    git url: "https://github.com/anand123hai/calculator.git"
                }
            }
            stage("Compile") {
                steps {
                    bat "mvn compile"
                }
            }
            stage("Unit test") {
                steps {
                    bat "mvn test"
                }
            }
            stage("Code coverage-JaCoCo") {
                steps {
                    bat "mvn install"
                    publishHTML (target: [
                        reportDir: 'site/jacoco',
                        reportFiles: 'index.html',
                        reportName: "JaCoCo Report"
                        ])
                }
            }
        }
    }