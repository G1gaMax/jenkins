pipeline {
    agent any

    environment {
        USER_CREDENTIALS = credentials('aws')
    }
    
     tools {
        terraform 'terraform'
    }


    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/maxi20222/jenkins.git'
            }
        }

        stage('Initialize') {
            steps {
                script {
                    // Initialize Terraform
                    sh 'terraform init'
                }
            }
        }

        stage('Validate') {
            steps {
                script {
                    // Validate Terraform code
                    sh 'terraform validate'
                }
            }
        }

        stage('Plan') {
            steps {
                script {
                    // Generate and show Terraform plan
                    sh 'terraform plan -out=tfplan'
                }
            }
        }

        stage('Apply') {
            steps {
                script {
                    // Generate and show Terraform plan
                     sh 'terraform apply -auto-approve tfplan'
                }
            }
        }


        stage('Configure Nginx') {
            steps {
                script {
                    // Run Ansible playbook to configure Nginx
                    sh 'ansible-playbook -i ${instance_dns}, -u ec2-user --private-key=$USER_CREDENTIALS nginx_install_playbook.yml'
                }
            }
        }
    }
    }
