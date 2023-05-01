pipeline {
    agent any
    triggers{ pollSCM('*/1 * * * *') }


    stages {
        stage('Build') {
            steps {
                script{
                    build()
                }
            }
        }
        stage('Deploy to DEV') {
            steps {
                script{
                    deploy("DEV", 1010)
                }
            }
        }
        stage('Tests on DEV') {
            steps {
                script{
                    test("DEV")
                }
            }
        }
        stage('Deploy to STG') {
            steps {
                script{
                    deploy("STG", 2020)
                }
            }
        }
        stage('Tests on STG') {
            steps {
                script{
                    test("STG")
                }
            }
        }
        stage('Deploy to PRD') {
            steps {
                script{
                    deploy("PRD", 3030)
                }
            }
        }
        stage('Tests on PRD') {
            steps {
                script{
                    test("PRD")
                }
            }
        }
    }
}

// for windows: bat "npm.."
// for linux/macos: sh "npm .."

def build(){
    echo "Building of node application is starting.."
    bat "npm install"
}

def deploy(String environment, int port){
    echo "Deployment to ${environment} has started.."
    bat "node_modules/.bin/pm2 delete \"books-${environment}\""
    bat "node_modules/.bin/pm2 start -n \"books-${environment}\" index.js -- ${port}"
}

def test(String environment){
    echo "Testing to ${environment} has started.."
}

// Būvējuma izveidi;
// Būvējuma izvietošanu “DEV” vidē;
// Testu izpildi “DEV” vidē;
// Būvējuma izvietošanu “STG” vidē;
// Testu izpildi “STG” vidē;
// Būvējuma izvietošanu “PRD” vidē;
// Testu izpildi “PRD” vidē;
