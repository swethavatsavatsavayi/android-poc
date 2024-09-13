pipeline {
    agent any
    environment {
        ANDROID_HOME = "/home/svatsavayi/android-sdk/"  // Replace with your actual Android SDK path
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-17.0.12.0.7-2.el8.x86_64"  // Replace with your actual Java SDK path
        FASTLANE_HOME = "/usr/local/rvm/gems/ruby-3.3.0/gems/fastlane-2.222.0/bin/"
        PATH = "$FASTLANE_HOME:$PATH"
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