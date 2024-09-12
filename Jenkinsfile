pipeline {
    agent any
    environment {
        ANDROID_HOME = "/home/android-sdk"  // Replace with your actual Android SDK path
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64/"  // Replace with your actual Java SDK path
        // PATH = "$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools:$PATH"
    }
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout code from your version control system
               checkout scm
               sh 'chmod +x gradlew'
            }
        }

        // stage('Install Dependencies') {
        //     steps {
        //         // Install dependencies
        //         sh 'npm install'
        //     }
        // }

        stage('Run Fastlane') {
            steps {
                // Build the APK using Fastlane
                sh 'fastlane android build_apk'
            }
        }

        stage('Archive APK') {
            steps {
                // Archive the APK as an artifact in Jenkins
                archiveArtifacts artifacts: 'android/app/build/outputs/apk/release/app-release.apk', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            echo 'APK build successful!'
        }
        failure {
            echo 'APK build failed.'
        }
    }
}