pipeline {
    agent { label 'local-agent' }
    environment {
        ID_RSA = "${env.ID_RSA}"
        PROD_SERVER_IP = "${env.PROD_SERVER_IP}"
        PROD_SERVER_USER = "${env.PROD_SERVER_USER}"
        PROD_SUDO_PASS = "${env.PROD_SUDO_PASS}"
    }
    stages {
        stage('Check ENV') {
            steps {
                script {
                     sh "cat hosts.txt"
                }
            }
        }         
        stage('Run Ansible Playbook') {
            steps {
                script {
                    sh '''
                    ansible-playbook -i hosts.txt ansible_/docker_setup.yml \
                    --extra-vars "ansible_ssh_private_key_file=$ID_RSA \
                    prod_server_ip=$PROD_SERVER_IP \
                    prod_server_user=$PROD_SERVER_USER \
                    prod_sudo_pass=$PROD_SUDO_PASS"
                    '''
                }
            }
        }
    }
}
