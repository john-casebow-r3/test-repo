
//
// Basic Jenkins pipeline that checks out the Greenium codebase, builds the code, runs tests & integrationTests and publishes reports
//

pipeline {

    agent any

    triggers {
        pollSCM('* * * * *') //polling for changes, here once a minute
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'Jenkins', url: 'https://github.com/john-casebow-r3/greenium']]])
            }
        }

        stage('Build') {
            steps {
                withGradle {
                    sh './gradlew clean build'
                }
            }
        }

        stage('IntegrationTest') {
            steps {
                withGradle {
                    sh './gradlew integrationTest'
                }
            }
        }
    }

    post {
        always {
            junit '**/test/*.xml'
            junit '**/integrationTest/*.xml'
            jacoco classPattern: "**/*/classes", sourcePattern: "**/src/main/kotlin"
        }
    }
}