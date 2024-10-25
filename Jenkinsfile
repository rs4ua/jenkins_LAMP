pipeline {
    agent { label 'local-agent' }
//*****************************************************************************************************************************************************************
    environment {
        INVENTORY_FILE = 'ansible_/hosts.txt'
        PLAYBOOK_FILE = 'ansible_/ansible-playbook.yml'
//*****************************************************************************************************************************************************************
        DOCKER_IMAGE_NAME_1 = 'back1'
        DOCKER_IMAGE_NAME_2 = 'back2'
        DOCKER_IMAGE_NAME_3 = 'back2'
        DOCKER_IMAGE_NAME_4 = 'ngx'
        DOCKER_IMAGE_VERSION = "1.${env.BUILD_NUMBER}"
        PREVIOUS_DOCKER_IMAGE_VERSION = "1.${env.BUILD_NUMBER.toInteger() - 1}"
        NEXUS_URL = '192.168.1.72:8082'
        NEXUS_REPOSITORY = 'repository/docker-host'
    }
    
//*****************************************************************************************************************************************************************
    stages {
//*****************************************************************************************************************************************************************
        
                stage('Create and Send Docker Image to Nexus') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'nexusCredential', usernameVariable: 'NEXUS_USERNAME', passwordVariable: 'NEXUS_PASSWORD')]) {
                        def dockerImageTag = "${DOCKER_IMAGE_NAME_1}:${DOCKER_IMAGE_VERSION}"
                        def nexusRepositoryTag = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag}"
                        
                        // Login to Nexus Docker registry
                        sh "echo ${NEXUS_PASSWORD} | docker login ${NEXUS_URL} -u ${NEXUS_USERNAME} --password-stdin"
                        
                        // Build and push the image to Nexus
                        sh """
                          docker build --no-cache -t ${dockerImageTag} .
                          docker tag ${dockerImageTag} ${NEXUS_URL}/${NEXUS_REPOSITORY}/${DOCKER_IMAGE_NAME_1}:${DOCKER_IMAGE_VERSION}
                          docker push ${NEXUS_URL}/${NEXUS_REPOSITORY}/${DOCKER_IMAGE_NAME_1}:${DOCKER_IMAGE_VERSION}
                        """
                    }
                }
            }
        }
        
//*****************************************************************************************************************************************************************
        
        stage('Stop and Remove Old Container and Image') {
            steps {
                script {
                    // Stop and remove the old container if it exists
                    sh "docker stop my-httpd || true"
                    sh "docker rm my-httpd || true"
                }
            }
        }
        
//*****************************************************************************************************************************************************************

        stage('Remove Docker Image from Local Repository') {
           steps {
                script {
                    def dockerImageTag = "${DOCKER_IMAGE_NAME_1}:${DOCKER_IMAGE_VERSION}"
                    def dockerNexusImageTag = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag}"

                    // Remove local image
                    sh "docker rmi ${dockerImageTag}"
                    sh "docker rmi ${dockerNexusImageTag}"
               }
            }
        }
        
//*****************************************************************************************************************************************************************
        
        stage('Remove Previous Docker Image') {
            steps {
                script {
                    def dockerPreviosImageTag = "${DOCKER_IMAGE_NAME_1}:${PREVIOUS_DOCKER_IMAGE_VERSION}"
                    def previousNexusImageTag = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerPreviosImageTag}"

                    sh "docker rmi ${previousNexusImageTag} || true"
                }
            }
        }
        
//*****************************************************************************************************************************************************************
        
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
    
//*****************************************************************************************************************************************************************
    
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
