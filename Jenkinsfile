pipeline {
    agent any
    environment {
        ANDROID_HOME = "/home/svatsavayi/android-sdk/"  // Replace with your actual Android SDK path
        JAVA_HOME = "/usr/lib/jvm/java-11-openjdk-11.0.24.0.8-3.el8.x86_64"  // Replace with your actual Java SDK path
        //HOME = "/home/svatsavayi/.rvm/gems/ruby-3.3.0/gems/fastlane-2.222.0/"
        // PATH = "/home/svatsavayi/.rvm/gems/ruby-3.3.0/gems/fastlane-2.222.0/bin:" +
        //        "/home/svatsavayi/.rvm/gems/ruby-3.3.0/bin:" +
        //        "/home/svatsavayi/.rvm/gems/ruby-3.3.0@global/bin:" +
        //        "/home/svatsavayi/.rvm/rubies/ruby-3.3.0/bin:" +
        //        "/usr/local/bin:" +
        //        "$PATH"
        PATH = "/home/svatsavayi/.gem/ruby/gems/fastlane-2.206.2/bin/:$PATH"
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