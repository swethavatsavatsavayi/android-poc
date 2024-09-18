pipeline {
    agent any
    environment {
        ANDROID_HOME = "/home/svatsavayi/android-sdk/"  //  actual Android SDK path
        JAVA_HOME = "/usr/lib/jvm/java-1.8.0"  //  actual Java SDK path
        PATH = "/usr/local/rvm/gems/ruby-3.3.0/bin:/usr/local/rvm/gems/ruby-3.3.0@global/bin:/usr/local/rvm/rubies/ruby-3.3.0/bin:/usr/local/rvm/bin:$PATH"
        //PATH = "/usr/local/rvm/gems/ruby-3.3.0/bin:" +
        //        "/usr/local/rvm/gems/ruby-3.3.0@global/bin:" +
        //        "/usr/local/rvm/gems//ruby-3.3.0/bin:" +
        //        "/usr/local/bin:" +
        //        "$PATH"
        //PATH = "/home/svatsavayi/.gem/ruby/gems/fastlane-2.206.2/bin/:$PATH"
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
                sh 'echo $PATH'
                sh 'bundle install'
                sh 'bundle exec fastlane android build_apk'
            }
        }
        stage('Archive APK') {
            steps {
                // Archive the APK as an artifact in Jenkins
                archiveArtifacts artifacts: 'app/build/outputs/apk/release/app-release.aab', allowEmptyArchive: true
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