pipeline {
    agent {label "agent-node"}
    stages {
        stage('Continous Integration') {
            steps {
                git branch: 'main', url: 'https://github.com/JossBvd/nodeJS_frontend_example'
            }
        }
        stage('Deploy via FTP') {
            steps {
                sh '''
                    lftp -d -u jocelyn2,n8664f6y ftp-jocelyn2.alwaysdata.net -e "
                        mirror -R /home/jenkins/workspace/jocelyn-test-front/ www/;
                        bye
                    "
                '''
            }
        }
        stage('Install NPM') {
            steps {
                sh """
                    sshpass -p n8664f6y ssh -o StrictHostKeyChecking=no jocelyn2@ssh-jocelyn2.alwaysdata.net \\
                    "cd ~/www && npm install"
                """
            }
        }

    }
}
