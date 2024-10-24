pipeline {
    agent { label 'local-agent' }

    environment {
        // Define environment variables for inventory and playbook files
        INVENTORY_FILE = 'ansible_/hosts.txt'
        PLAYBOOK_FILE = 'ansible_/ansible-playbook.yml'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // List files to confirm the repository is cloned
                sh "ls -l"
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                // Access the ANSIBLE_SECRET_TEXT from Jenkins credentials
                withCredentials([string(credentialsId: 'ANSIBLE_SECRET_TEXT', variable: 'VAULT_PASS')]) {
                    // Write the vault password to a temporary file
                    script {
                        def vaultPasswordFile = 'vault_password.txt'
                        writeFile file: vaultPasswordFile, text: "${VAULT_PASS}"
                        sh "ansible-playbook -i ${INVENTORY_FILE} ${PLAYBOOK_FILE} --vault-password-file ${vaultPasswordFile} --extra-vars secret_text=\$VAULT_PASS"
                    }
                }
            }
        }
    }

    post {
        always {
            sh "rm -f vault_password.txt" // Cleanup the temporary vault password file
        }
        success {
            echo 'Playbook executed successfully!'
        }
        failure {
            echo 'Failed to execute playbook.'
        }
    }
}
