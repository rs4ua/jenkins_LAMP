pipeline {
    agent { label 'local-agent' }

    environment {
        INVENTORY_FILE = 'ansible_/hosts.txt'
        PLAYBOOK_FILE = 'ansible_/ansible-playbook.yml'
        DOCKER_IMAGE_NAMES = ['back1', 'back2', 'back3', 'nginx']
        DOCKER_IMAGE_VERSION = "1.${env.BUILD_NUMBER}"
        PREVIOUS_DOCKER_IMAGE_VERSION = "1.${env.BUILD_NUMBER.toInteger() - 1}"
        NEXUS_URL = '192.168.1.72:8082'
        NEXUS_REPOSITORY = 'repository/docker-host'
        REMOTE_SERVER = '192.168.1.128'
        SSH_CREDENTIALS_ID = 'ssh_prod_srv'
    }

    stages {
        // Stage to build and push Docker images to Nexus
        stage('Build and Push Docker Images to Nexus') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'nexusCredential', usernameVariable: 'NEXUS_USERNAME', passwordVariable: 'NEXUS_PASSWORD')]) {
                        DOCKER_IMAGE_NAMES.each { imageName ->
                            def dockerImageTag = "${imageName}:${DOCKER_IMAGE_VERSION}"
                            def nexusRepositoryTag = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${dockerImageTag}"

                            // Login to Nexus Docker registry
                            sh "echo ${NEXUS_PASSWORD} | docker login ${NEXUS_URL} -u ${NEXUS_USERNAME} --password-stdin"

                            // Build and push the image to Nexus
                            sh """
                                docker build --no-cache -t ${dockerImageTag} ./${imageName}
                                docker tag ${dockerImageTag} ${nexusRepositoryTag}
                                docker push ${nexusRepositoryTag}
                            """
                        }
                    }
                }
            }
        }

        // Stage to remove Docker images from local repository
        stage('Remove Docker Images from Local Repository') {
            steps {
                script {
                    DOCKER_IMAGE_NAMES.each { imageName ->
                        def dockerImageTag = "${imageName}:${DOCKER_IMAGE_VERSION}"
                        sh "docker rmi ${dockerImageTag} || true"
                    }
                }
            }
        }

        // Stage to pull Docker images from Nexus on remote server
        stage('Pull Images from Nexus on Remote Server') {
            steps {
                script {
                    DOCKER_IMAGE_NAMES.each { imageName ->
                        def nexusRepositoryTag = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${imageName}:${DOCKER_IMAGE_VERSION}"
                        sshagent([SSH_CREDENTIALS_ID]) {
                            sh "ssh ${REMOTE_SERVER} 'docker pull ${nexusRepositoryTag} || true'"
                        }
                    }
                }
            }
        }

        // Stage to generate Docker Compose file
        stage('Generate Docker Compose File') {
            steps {
                script {
                    def dockerComposeContent = """
version: '3'
services:
  nginx:
    image: ${NEXUS_URL}/${NEXUS_REPOSITORY}/nginx:${DOCKER_IMAGE_VERSION}
    container_name: nginx-front
    restart: always
    ports:
      - "80:80"
      - "443:443"

  backend1:
    image: ${NEXUS_URL}/${NEXUS_REPOSITORY}/back1:${DOCKER_IMAGE_VERSION}
    container_name: back1_container
    restart: always

  backend2:
    image: ${NEXUS_URL}/${NEXUS_REPOSITORY}/back2:${DOCKER_IMAGE_VERSION}
    container_name: back2_container
    restart: always

  backend3:
    image: ${NEXUS_URL}/${NEXUS_REPOSITORY}/back3:${DOCKER_IMAGE_VERSION}
    container_name: back3_container
    restart: always

networks:
  front:
  backend:
"""
                    // Write the docker-compose.yml file
                    writeFile file: 'docker-compose.yml', text: dockerComposeContent
                }
            }
        }

        // Stage to deploy Docker Compose on remote server
        stage('Deploy Docker Compose on Remote Server') {
            steps {
                script {
                    sshagent([SSH_CREDENTIALS_ID]) {
                        // Copy docker-compose.yml to the remote server
                        sh "scp docker-compose.yml ${SSH_CREDENTIALS_ID}@${REMOTE_SERVER}:/home/user/"

                        // Run docker-compose up on the remote server
                        sh "ssh ${REMOTE_SERVER} 'docker-compose -f /home/user/docker-compose.yml up -d'"
                    }
                }
            }
        }

        // Stage to remove previous Docker images on remote server
        stage('Remove Previous Docker Images') {
            steps {
                script {
                    DOCKER_IMAGE_NAMES.each { imageName ->
                        def previousNexusImageTag = "${NEXUS_URL}/${NEXUS_REPOSITORY}/${imageName}:${PREVIOUS_DOCKER_IMAGE_VERSION}"
                        sshagent([SSH_CREDENTIALS_ID]) {
                            sh "ssh ${REMOTE_SERVER} 'docker rmi ${previousNexusImageTag} || true'"
                        }
                    }
                }
            }
        }
    }
}
