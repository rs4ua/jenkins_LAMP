pipeline {
    agent { label 'local-agent' }
    environment {
        ANSIBLE_USER = 'user'
        ANSIBLE_SUDO_PASS = 'roMashka'
        ANSIBLE_SSH_PRIVATE_KEY = '''
        -----BEGIN OPENSSH PRIVATE KEY-----
        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
        AwQFBg==
        -----END OPENSSH PRIVATE KEY-----
        '''
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
