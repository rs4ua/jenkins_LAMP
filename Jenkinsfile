pipeline {
    agent { label 'local-agent' } // Replace with your agent label
    stages {
        stage('List Files') {
            steps {
                // List files in the ansible_ directory to verify inventory location
                sh 'ls -l ansible_/' // Adjust the path as needed
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Define the inventory and playbook file paths
                    def inventoryFile = 'ansible_/hosts.thx' // Path to your inventory file in the repo
                    def playbookFile = 'ansible_/docker_setup.yml' // Path to your playbook file in the repo

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
