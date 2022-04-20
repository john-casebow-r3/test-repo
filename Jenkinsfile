
//
// Basic Jenkins pipeline that checks out the Greenium codebase, builds the code, runs tests & integrationTests and publishes reports
//

pipeline {

    agent any

    triggers {
        pollSCM('* * * * *') //polling for changes, here once a minute
    }

    stages {
        stage('Build') {
            steps {
                withGradle {
                    sh './gradlew clean build --stacktrace --info'
                }
                junit '**/test/*.xml'
                jacoco classPattern: "**/*/classes", sourcePattern: "**/src/main/kotlin"
            }
        }
    }
}
