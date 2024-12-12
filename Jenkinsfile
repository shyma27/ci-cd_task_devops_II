pipeline {
    agent any

    stages {
        stage('Install Apache2') {
            steps {
                // install apache2 and check it's status
                sh 'sudo apt install apache2'
                sh 'sudo systemctl status apache2'
            }
        }
        stage('Check Apache2 logs') {
            steps {
                script {
                    // check logs with Grep
                    //sh(script: 'sudo grep " 4[0-9][0-9] " /var/log/apache2/access.log', returnStatus: true)
                    //sh(script: 'sudo grep " 5[0-9][0-9] " /var/log/apache2/access.log', returnStatus: true)
                    def error_4xx = 'sudo grep " 4[0-9][0-9] " /var/log/apache2/access.log'
                    def error_5xx = 'sudo grep " 5[0-9][0-9] " /var/log/apache2/access.log'
                    def arr = [error_4xx, error_5xx]

                    for (int i = 0; i < arr.length; i++) {
                        try {
                            sh "${arr[i]}"
                            // echo 'Succeeded!'
                        } catch (err) {
                            echo "Logs are absent for ${arr[i]}"
                        }
                    }
                } 
            }
        }
    }
}
