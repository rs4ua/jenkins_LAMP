pipeline {
    agent { label 'local-agent' }

    environment {
        // Define an environment variable for the inventory file or other configs
        INVENTORY_FILE = 'ansible_/hosts.txt'
        PLAYBOOK_FILE = 'ansible_/ansible-playbook.yml'
    }

    stages {
        stage('Clone Repository') {
            steps {
                sh "ls -R"
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                // Access the ANSIBLE_SECRET_TEXT from Jenkins credentials
                withCredentials([string(credentialsId: 'ANSIBLE_SECRET_TEXT', variable: 'ANSIBLE_SECRET_TEXT')]) {
                    
                    // Run the Ansible playbook and pass the secret as needed
                    sh '''
                    ansible-playbook -i ${INVENTORY_FILE} ${PLAYBOOK_FILE} --extra-vars "secret_text=$ANSIBLE_SECRET_TEXT"
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Playbook executed successfully!'
        }
        failure {
            echo 'Failed to execute playbook.'
        }
    }
}
