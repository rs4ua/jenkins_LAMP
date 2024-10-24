pipeline {
    agent { label 'local-agent' } // Replace with your agent label
    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from GitHub
                git url: 'https://github.com/rs4ua/jenkins_LAMP.git', branch: 'main' // Replace with your repository URL and branch
            }
        }
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
                    def inventoryFile = 'ansible_/hosts.txt' // Path to your inventory file in the repo
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

