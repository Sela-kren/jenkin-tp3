pipeline {
    agent any // windows agent, Jenkins-Laravel (other machine)
    
    stages {
        stage('Fetch from GitHub') { // build steps
            steps {
                echo 'Fetching from GitHub'
                git branch: 'TP2', url:'https://github.com/LengSokchhay/Jenkin.git'
            }
        }
        stage('Build using Tools') {
            steps {
                echo 'Compiling code...'
                sh 'cp .env.example .env'
                sh 'composer install && php artisan key:generate && npm install && npm run build'
            }
        }
        stage('Test the app') {
            steps {
                echo 'Testing unit tests...'
                echo 'Testing features...'
                sh 'php artisan test1'
            }
        }
        stage('Email Notification'){
                mail bcc: '', body: '''Hi, Welcome to Jenkins Alert
                The build is failure.''', cc: '', from: '', replyTo: '', subject: 'Jenkins job', to: 'mastersokchhayfap@gmail.com'
        }
    }
    post {
        
        failure {
            echo 'sending email notification from jenkins'
            
            step([$class: 'Mailer',
      notifyEveryUnstableBuild: true,
      recipients: emailextrecipients([[$class: 'CulpritsRecipientProvider'],
                                      [$class: 'RequesterRecipientProvider']])])

            
       }
    }
}