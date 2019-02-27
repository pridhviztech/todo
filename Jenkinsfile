pipeline {
    agent any
    stages {
        stage('build') {
            input {
                message "Press OK to initiate the build"
            }
            steps {
                sh 'nohup ionic serve &'
            }
        }
    }
    post {
        success {
            sh 'cp -r www/* /var/www/html/'
        }
        always {
            emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
    }
}
