pipeline {
    agent any
    environment {
        ANDROID_HOME = "/home/svatsavayi/android-sdk/"  //  actual Android SDK path
        JAVA_HOME = "/usr/lib/jvm/java-1.8.0"  //  actual Java SDK path
        PATH = "/home/svatsavayi/.rvm/gems/ruby-3.3.0/gems/fastlane-2.222.0/bin:" +
               "/home/svatsavayi/.rvm/gems/ruby-3.3.0/bin:" +
               "/home/svatsavayi/.rvm/gems/ruby-3.3.0@global/bin:" +
               "/home/svatsavayi/.rvm/rubies/ruby-3.3.0/bin:" +
               "/usr/local/bin:" +
               "$PATH"
        //PATH = "/home/svatsavayi/.gem/ruby/gems/fastlane-2.206.2/bin/:$PATH"
    }
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout code from your version control system
               checkout scm
               sh 'chmod 777 -R .'
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
                sh 'echo $JAVA_HOME'
                sh 'fastlane -v'
                sh 'fastlane env'
                sh 'fastlane android build_apk'
            }
        }
        stage('Archive APK') {
            steps {
                // Archive the APK as an artifact in Jenkins
                archiveArtifacts artifacts: 'android/app/build/outputs/apk/release/app-release.aab', allowEmptyArchive: true
            }
        }
    }
    post {
        success {
            echo 'Android build successful!'
        }
        failure {
            echo 'Android build failed.'
        }
    }
}