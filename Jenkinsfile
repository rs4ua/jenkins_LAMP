pipeline {
    agent { label 'local-agent' } // Specify the agent to run the pipeline

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository containing your Ansible playbook
                git url: 'https://github.com/your_username/your_repository.git', branch: 'main' // Update with your repo URL and branch
            }
        }

        stage('Setup') {
            steps {
                // Install required Ansible collections if needed
                sh 'ansible-galaxy collection install community.general'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                // Run the Ansible playbook
                ansiblePlaybook(
                    playbook: 'files/docker_setup.yml', // Path to your Ansible playbook
                    inventory: 'files/hosts.txt', // Path to your inventory file
                    extras: '-i files/hosts.txt', // Extra arguments if necessary
                    colorized: true // Optional, for better output formatting
                )
            }
        }
    }

    post {
        always {
            // Clean up workspace after build
            cleanWs()
        }
    }
}
