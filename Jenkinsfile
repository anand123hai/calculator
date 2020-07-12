pipeline {
    agent {label "centos-slave"}
    stages {
            stage("Checkout") {
                steps {
                    git branch: 'feature', credentialsId: 'github-credentials-anand123hai-global', url: 'https://github.com/anand123hai/calculator.git'
                }
            }
            stage("Compile") {
                steps {
                    sh "mvn compile"
                }
            }
            stage("Unit test") {
                steps {
                    sh "mvn test"
                }
            }
            stage("Package") {
                steps {
                    sh "mvn package"
                }
            }
            stage("Docker build image") {
                steps {
                    sh "docker build -t anand123hai/calculator ."
                }
            }
            stage("Docker push") {
                steps {
                    sh "docker login -u anand123hai -p Docker@123.ag"
                    sleep 10
                    sh "docker push anand123hai/calculator"
                }
            }
            stage("Deploy to staging") {
                steps {
                    sh "docker run -d --rm -p 8765:8080 --name calculator anand123hai/calculator"
                }
            }
            stage("Acceptance test") {
                steps {
                    sleep 60
                    sh "./acceptance_test.sh"
                }
            }
        }
        post { always { sh "docker stop calculator" } }
    }