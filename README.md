Yii2 Swarm Demo

This repository demonstrates deploying a minimal Yii2 PHP application using Docker Swarm, NGINX, Ansible, and GitHub Actions on an AWS EC2 instance.

Prerequisites





AWS EC2 instance (Ubuntu 22.04)



SSH key pair



Docker Hub account



GitHub repository: ajay8297/yii2-swarm-demo

Setup Instructions





EC2 Setup





Launch an EC2 instance (t2.micro or larger).



Open ports 80 (HTTP), 9090 (Prometheus), and 22 (SSH) in the security group.



GitHub Secrets





Add the following to your repository secrets:





DOCKER_USERNAME: Docker Hub username



DOCKER_PASSWORD: Docker Hub access token



EC2_HOST: EC2 public IP



EC2_USERNAME: EC2 username (e.g., ubuntu)



EC2_SSH_KEY: EC2 private SSH key



Ansible Setup





Install Ansible locally: pip install ansible



Update ansible/hosts with your EC2 IP:

[servers]
<EC2_PUBLIC_IP> ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/<your-key>.pem



Run the playbook:

ansible-playbook -i ansible/hosts ansible/playbook.yml



Push Code





Push changes to the main branch to trigger the GitHub Actions workflow.

Testing





Visit http://<EC2_PUBLIC_IP> to see the Yii2 app.



Visit http://<EC2_PUBLIC_IP>/prometheus for monitoring.



Check Docker Swarm: ssh ubuntu@<EC2_PUBLIC_IP> 'docker stack ps yii2'.

Assumptions





Single-node Docker Swarm.



NGINX runs on the host as a reverse proxy.



Prometheus and Node Exporter for basic monitoring.



Health checks in Docker Compose.



No rollback mechanism (kept minimal).

Monitoring





Prometheus: http://<EC2_PUBLIC_IP>/prometheus



Node Exporter metrics are scraped every 15 seconds.
