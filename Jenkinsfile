pipeline {
    agent { label 'local-agent' }
//*****************************************************************************************************************************************************************
    environment {
        INVENTORY_FILE = 'ansible_/hosts.txt'
        PLAYBOOK_FILE = 'ansible_/ansible-playbook.yml'
//*****************************************************************************************************************************************************************
        DOCKER_IMAGE_NAME_1 = 'back1'
        DOCKER_IMAGE_NAME_2 = 'back2'
        DOCKER_IMAGE_NAME_3 = 'back3'
        DOCKER_IMAGE_NAME_4 = 'nginx'
        DOCKER_IMAGE_VERSION = "1.${env.BUILD_NUMBER}"
        PREVIOUS_DOCKER_IMAGE_VERSION = "1.${env.BUILD_NUMBER.toInteger() - 1}"
        NEXUS_URL = '192.168.1.72:8082'
        NEXUS_REPOSITORY = 'repository/docker-host'
    }
    
//*****************************************************************************************************************************************************************
    stages {
//*****************************************************************************************************************************************************************
        
// Stage for DOCKER_IMAGE_NAME_1 (back1 folder)
        stage('Create and Send Docker Image to Nexus - Image 1') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'nexusCredential', usernameVariable: 'NEXUS_USERNAME', passwordVariable: 'NEXUS_PASSWORD')]) {
                        def dockerImageTag = "${DOCKER_IMAGE_NAME_1}:${DOCKER_IMAGE_VERSION}"
                        def nexusRepositoryTag = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag}"

                        // Login to Nexus Docker registry
                        sh "echo ${NEXUS_PASSWORD} | docker login ${NEXUS_URL} -u ${NEXUS_USERNAME} --password-stdin"
                        
                        // Build and push the image to Nexus
                        sh """
                          docker build --no-cache -t ${dockerImageTag} ./back1
                          docker tag ${dockerImageTag} ${nexusRepositoryTag}
                          docker push ${nexusRepositoryTag}
                        """
                    }
                }
            }
        }

        // Repeat for DOCKER_IMAGE_NAME_2 (back2 folder)
        stage('Create and Send Docker Image to Nexus - Image 2') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'nexusCredential', usernameVariable: 'NEXUS_USERNAME', passwordVariable: 'NEXUS_PASSWORD')]) {
                        def dockerImageTag = "${DOCKER_IMAGE_NAME_2}:${DOCKER_IMAGE_VERSION}"
                        def nexusRepositoryTag = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag}"

                        // Login to Nexus Docker registry
                        sh "echo ${NEXUS_PASSWORD} | docker login ${NEXUS_URL} -u ${NEXUS_USERNAME} --password-stdin"
                        
                        // Build and push the image to Nexus
                        sh """
                          docker build --no-cache -t ${dockerImageTag} ./back2
                          docker tag ${dockerImageTag} ${nexusRepositoryTag}
                          docker push ${nexusRepositoryTag}
                        """
                    }
                }
            }
        }

        // Repeat for DOCKER_IMAGE_NAME_3 (back3 folder)
        stage('Create and Send Docker Image to Nexus - Image 3') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'nexusCredential', usernameVariable: 'NEXUS_USERNAME', passwordVariable: 'NEXUS_PASSWORD')]) {
                        def dockerImageTag = "${DOCKER_IMAGE_NAME_3}:${DOCKER_IMAGE_VERSION}"
                        def nexusRepositoryTag = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag}"

                        // Login to Nexus Docker registry
                        sh "echo ${NEXUS_PASSWORD} | docker login ${NEXUS_URL} -u ${NEXUS_USERNAME} --password-stdin"
                        
                        // Build and push the image to Nexus
                        sh """
                          docker build --no-cache -t ${dockerImageTag} ./back3
                          docker tag ${dockerImageTag} ${nexusRepositoryTag}
                          docker push ${nexusRepositoryTag}
                        """
                    }
                }
            }
        }

        // Repeat for DOCKER_IMAGE_NAME_4 (nginx folder)
        stage('Create and Send Docker Image to Nexus - Image 4') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'nexusCredential', usernameVariable: 'NEXUS_USERNAME', passwordVariable: 'NEXUS_PASSWORD')]) {
                        def dockerImageTag = "${DOCKER_IMAGE_NAME_4}:${DOCKER_IMAGE_VERSION}"
                        def nexusRepositoryTag = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag}"

                        // Login to Nexus Docker registry
                        sh "echo ${NEXUS_PASSWORD} | docker login ${NEXUS_URL} -u ${NEXUS_USERNAME} --password-stdin"
                        
                        // Build and push the image to Nexus
                        sh """
                          docker build --no-cache -t ${dockerImageTag} ./nginx
                          docker tag ${dockerImageTag} ${nexusRepositoryTag}
                          docker push ${nexusRepositoryTag}
                        """
                    }
                }
            }
        }
            
//*****************************************************************************************************************************************************************

        stage('Remove Docker Images from Local Repository') {
           steps {
                script {
                    def dockerImageTag_1 = "${DOCKER_IMAGE_NAME_1}:${DOCKER_IMAGE_VERSION}"
                    def dockerNexusImageTag_1 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag_1}"
                    def dockerImageTag_2 = "${DOCKER_IMAGE_NAME_2}:${DOCKER_IMAGE_VERSION}"
                    def dockerNexusImageTag_2 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag_2}"
                    def dockerImageTag_3 = "${DOCKER_IMAGE_NAME_3}:${DOCKER_IMAGE_VERSION}"
                    def dockerNexusImageTag_3 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag_3}"
                    def dockerImageTag_4 = "${DOCKER_IMAGE_NAME_4}:${DOCKER_IMAGE_VERSION}"
                    def dockerNexusImageTag_4 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag_4}"

                    // Remove local images
                    sh "docker rmi ${dockerImageTag_1}"
                    sh "docker rmi ${dockerNexusImageTag_1}"
                    sh "docker rmi ${dockerImageTag_2}"
                    sh "docker rmi ${dockerNexusImageTag_2}"
                    sh "docker rmi ${dockerImageTag_3}"
                    sh "docker rmi ${dockerNexusImageTag_3}"
                    sh "docker rmi ${dockerImageTag_4}"
                    sh "docker rmi ${dockerNexusImageTag_4}"
               }
            }
        }
        
//*****************************************************************************************************************************************************************
        
        stage('Remove Previous Docker Images') {
            steps {
                script {
                    def dockerPreviosImageTag_1 = "${DOCKER_IMAGE_NAME_1}:${PREVIOUS_DOCKER_IMAGE_VERSION}"
                    def previousNexusImageTag_1 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerPreviosImageTag_1}"
                    def dockerPreviosImageTag_2 = "${DOCKER_IMAGE_NAME_2}:${PREVIOUS_DOCKER_IMAGE_VERSION}"
                    def previousNexusImageTag_2 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerPreviosImageTag_2}"
                    def dockerPreviosImageTag_3 = "${DOCKER_IMAGE_NAME_3}:${PREVIOUS_DOCKER_IMAGE_VERSION}"
                    def previousNexusImageTag_3 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerPreviosImageTag_3}"
                    def dockerPreviosImageTag_4 = "${DOCKER_IMAGE_NAME_4}:${PREVIOUS_DOCKER_IMAGE_VERSION}"
                    def previousNexusImageTag_4 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerPreviosImageTag_4}"

                    sh "docker rmi ${previousNexusImageTag_1} || true"
                    sh "docker rmi ${previousNexusImageTag_2} || true"
                    sh "docker rmi ${previousNexusImageTag_3} || true"
                    sh "docker rmi ${previousNexusImageTag_4} || true"
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
