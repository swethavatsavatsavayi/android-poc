pipeline {
    agent any
    environment {
        ANDROID_HOME = "/home/svatsavayi/android-sdk/"  //  actual Android SDK path
        JAVA_HOME = "/usr/lib/jvm/java-1.8.0"  //  actual Java SDK path
        PATH =  "$HOME/.fastlane/bin:" +
                "$HOME/.rvm/gems/ruby-2.6.3/bin:" +
                "$HOME/.rvm/gems/ruby-2.6.3@global/bin:" +
                "$HOME/.rvm/rubies/ruby-2.6.3/bin:" +
                "/usr/local/bin:" +
                "$PATH"
        //PATH = "/home/svatsavayi/.gem/ruby/gems/fastlane-2.206.2/bin/:$PATH"
    }
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout code from your version control system
               checkout scm
            //    sh 'chmod 777 -R .'
            //    sh 'gpg2 --keyserver hkp://keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB'
            //    sh 'curl -L get.rvm.io | bash -s stable'
            //    sh 'source /var/lib/jenkins/.rvm/scripts/rvm'
            //    sh 'cd /var/lib/jenkins/.rvm/scripts/'
            //    sh 'chmod +x -R .'
            //    sh 'rvm requirements'
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
                // sh 'echo $JAVA_HOME'
                // sh 'rvm -v'
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