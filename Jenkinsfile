pipeline {
    agent { label 'local-agent' } // Replace with your agent label
    stages {
        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Define the inventory and playbook file paths
                    def inventoryFile = 'ansible_/hosts.txt' // Correct path to your inventory file
                    def playbookFile = 'ansible_/ansible-playbook.yml' // Correct path to your playbook file
                    
                    // Check if inventory file exists
                    if (fileExists(inventoryFile)) {
                        // Run the Ansible playbook
                        sh "ansible-playbook -i ${inventoryFile} ${playbookFile}"
                    } else {
                        error "Inventory file ${inventoryFile} not found. Please check the path."
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'Ansible playbook executed successfully!'
        }
        failure {
            echo 'Ansible playbook execution failed!'
        }
    }
}

