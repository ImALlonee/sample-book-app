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
                    test("DEV", "BOOKS")
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
                    test("STG", "BOOKS")
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
                    test("PRD", "BOOKS")
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
    // bat "npm test"
}

def deploy(String environment, int port){
    echo "Deployment to ${environment} has started.."
    git branch: 'main', url: 'https://github.com/ImALlonee/sample-book-app.git'
    bat "pm2 delete \"books-${environment}\""
    bat "pm2 start -n \"books-${environment}\" index.js -- ${port}"
}

def test(String environment, String test_set){
    echo "Testing ${test_set} test set to ${environment} has started.."
    git branch: 'main', poll: false, url: 'https://github.com/ImALlonee/course-js-api-framework.git'
    bat "dir"
    bat "npm install"
    bat "npm run ${test_set} ${test_set}_${environment}" 
}

// Būvējuma izveidi;
// Būvējuma izvietošanu “DEV” vidē;
// Testu izpildi “DEV” vidē;
// Būvējuma izvietošanu “STG” vidē;
// Testu izpildi “STG” vidē;
// Būvējuma izvietošanu “PRD” vidē;
// Testu izpildi “PRD” vidē;
