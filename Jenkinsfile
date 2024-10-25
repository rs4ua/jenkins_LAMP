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
        REMOTE_SERVER = '192.168.1.128'
        SSH_CREDENTIALS_ID = 'ssh_prod_srv'
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
                    sh """
                        docker rmi ${dockerImageTag_1}
                        docker rmi ${dockerNexusImageTag_1}
                        docker rmi ${dockerImageTag_2}
                        docker rmi ${dockerNexusImageTag_2}
                        docker rmi ${dockerImageTag_3}
                        docker rmi ${dockerNexusImageTag_3}
                        docker rmi ${dockerImageTag_4}
                        docker rmi ${dockerNexusImageTag_4}
                    """
               }
            }
        }
        
//*****************************************************************************************************************************************************************
        // Stage to pull Docker images from Nexus on remote server
        stage('Pull Image from Nexus') {
            steps {
                script {
                    def nexusRepositoryTag1 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${DOCKER_IMAGE_NAME_1}:${DOCKER_IMAGE_VERSION}"
                    def nexusRepositoryTag2 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${DOCKER_IMAGE_NAME_2}:${DOCKER_IMAGE_VERSION}"
                    def nexusRepositoryTag3 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${DOCKER_IMAGE_NAME_3}:${DOCKER_IMAGE_VERSION}"
                    def nexusRepositoryTag4 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${DOCKER_IMAGE_NAME_4}:${DOCKER_IMAGE_VERSION}"

                    // Use SSH to pull images on the remote server
                    sshagent([SSH_CREDENTIALS_ID]) {
                        sh """
                            ssh ${REMOTE_SERVER} 'docker pull ${nexusRepositoryTag1} || true'
                            ssh ${REMOTE_SERVER} 'docker pull ${nexusRepositoryTag2} || true'
                            ssh ${REMOTE_SERVER} 'docker pull ${nexusRepositoryTag3} || true'
                            ssh ${REMOTE_SERVER} 'docker pull ${nexusRepositoryTag4} || true'
                        """
                    }
                }
            }
        }
//*****************************************************************************************************************************************************************
        // Stage to remove old Docker images on remote server
        stage('Remove Previous Docker Images') {
            steps {
                script {
                    def previousNexusImageTag1 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${DOCKER_IMAGE_NAME_1}:${PREVIOUS_DOCKER_IMAGE_VERSION}"
                    def previousNexusImageTag2 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${DOCKER_IMAGE_NAME_2}:${PREVIOUS_DOCKER_IMAGE_VERSION}"
                    def previousNexusImageTag3 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${DOCKER_IMAGE_NAME_3}:${PREVIOUS_DOCKER_IMAGE_VERSION}"
                    def previousNexusImageTag4 = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${DOCKER_IMAGE_NAME_4}:${PREVIOUS_DOCKER_IMAGE_VERSION}"

                    // Use SSH to remove previous images on the remote server
                    sshagent([SSH_CREDENTIALS_ID]) {
                        sh """
                            ssh ${REMOTE_SERVER} 'docker rmi ${previousNexusImageTag1} || true'
                            ssh ${REMOTE_SERVER} 'docker rmi ${previousNexusImageTag2} || true'
                            ssh ${REMOTE_SERVER} 'docker rmi ${previousNexusImageTag3} || true'
                            ssh ${REMOTE_SERVER} 'docker rmi ${previousNexusImageTag4} || true'
                        """
                    }
                }
            }
        }
    }
}
