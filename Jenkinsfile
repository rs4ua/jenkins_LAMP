pipeline {
    agent { label 'local-agent' } // Replace with your agent label
    stages {
        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Define the inventory and playbook file paths
                    def inventoryFile = 'ansible_/hosts' // Path to your inventory file in the repo
                    def playbookFile = 'ansible_/docker_setup.yml' // Path to your playbook file in the repo

                    // Run the Ansible playbook
                    sh "ansible-playbook -i ${inventoryFile} ${playbookFile}"
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
