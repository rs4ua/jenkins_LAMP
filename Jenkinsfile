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
        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Running ansible-playbook
                    sh 'ansible-playbook -i ansible_/hosts.txt ansible_/ansible-playbook.yml'
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

