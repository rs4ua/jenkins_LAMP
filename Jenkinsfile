pipeline {
    agent { label 'local-agent' }
    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'false'
    }
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Prepare SSH Key') {
            steps {
                script {
                    // Write the private key to a file
                    writeFile file: 'ansible_/private_key.pem', text: "${ANSIBLE_SSH_PRIVATE_KEY}"
                    // Set proper permissions for the private key file
                    sh 'chmod 600 ansible_/private_key.pem'
                }
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Running ansible-playbook with the specified private key
                    sh 'ansible-playbook -i ansible_/hosts.txt --private-key ansible_/private_key.pem ansible_/ansible-playbook.yml'
                }
            }
        }
    }
    post {
        failure {
            echo 'Ansible playbook execution failed!'
        }
    }
}
