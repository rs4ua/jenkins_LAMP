pipeline {
    agent any
    environment {
        ID_RSA = "${env.ID_RSA}"
        PROD_SERVER_IP = "${env.PROD_SERVER_IP}"
        PROD_SERVER_USER = "${env.PROD_SERVER_USER}"
        PROD_SUDO_PASS = "${env.PROD_SUDO_PASS}"
    stages {
        stage('Run Ansible Playbook') {
            steps {
                script {
                    sh "ansible-playbook -i hosts.txt docker_setup.yml"
                }
            }
        }
    }
}

