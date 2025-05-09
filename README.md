
# Automated LAMP Stack Deployment Using Ansible on AWS EC2
Overview
This project automates the deployment of a LAMP stack (Linux, Apache, MySQL, PHP) on AWS EC2 instances running Ubuntu using Ansible. The goal is to streamline the setup process, which is often time-consuming and error-prone when done manually, by provisioning a fully functional LAMP stack with a single Ansible playbook. The automation configures the EC2 instance, installs and configures Apache, MySQL, and PHP, and sets up a sample PHP application to verify the deployment.
# Problem Statement
Manually configuring a LAMP stack on an EC2 instance involves multiple steps, including:
* Launching an EC2 instance.
* Installing and configuring Apache, MySQL, and PHP.
* Securing the server and database.
* Testing the setup.These steps are repetitive, prone to human error, and time-intensive, especially when deploying multiple instances or maintaining
  consistency across environments.

# Objective
The objective is to create an Ansible playbook that automates the provisioning and configuration of a LAMP stack on an Ubuntu-based AWS EC2 instance. The playbook ensures:
* Consistent and repeatable deployments.
* Minimal manual intervention.
* Secure configuration of the LAMP components.
* Verification of the setup with a sample PHP application.

# Solution Approach
The solution uses Ansible to orchestrate the deployment process on an AWS EC2 instance. The approach involves:
* EC2 Instance Setup: Configure an Ubuntu EC2 instance with appropriate security groups to allow HTTP and SSH access.
# Ansible Playbook: 
* Update the system and install required packages.
* Install and configure Apache as the web server.
* Install and secure MySQL with a preconfigured root password.
* Install PHP and necessary modules for Apache integration.
* Deploy a sample PHP application to verify the stack.

  ![ansible playbook](https://github.com/rukevweubio/Automated-LAMP-stack-deployment-using-Ansible-on-AWS-EC2-with-Apache-MySQL-PHP/blob/main/ansible/template/picture/Screenshot%20(678).png)


   ![ansible playbook](https://github.com/rukevweubio/Automated-LAMP-stack-deployment-using-Ansible-on-AWS-EC2-with-Apache-MySQL-PHP/blob/main/ansible/template/picture/Screenshot%20(679).png)


# Security Considerations:
Implement basic security measures, such as setting a MySQL root password and configuring Apache to run as a non-root user.
# Testing:
Deploy a sample PHP page to confirm that Apache, MySQL, and PHP are working together.

# Tools Used
* Ansible: Automation tool for orchestrating the deployment and configuration.
* AWS EC2: Cloud platform to host the Ubuntu server.
* Ubuntu 20.04 LTS: Operating system for the EC2 instance.
* Apache2: Web server to serve PHP applications.
* MySQL: Relational database management system.
* PHP: Server-side scripting language for dynamic web content.


Prerequisites
Before running the project, ensure you have:
* AWS Account with access to EC2.
* Ansible installed on your control machine (tested with Ansible 2.9+).
* SSH Key Pair for EC2 instance access.
* Python 3 and boto3 (for AWS integration, if using dynamic inventory).
* AWS CLI configured with credentials.

# Setup Instructions
Clone the Repository:
git clone 
cd automated-lamp-deployment


# Configure AWS EC2:
* Launch an Ubuntu 20.04 EC2 instance.
* Ensure the security group allows:
* Port 22 (SSH) for Ansible.
* Port 80 (HTTP) for Apache
  
# Update Inventory:

* Edit inventory.ini  to include your EC2 instance:all:
  ```
  hosts:
    lamp_server:
      ansible_host: <EC2_PUBLIC_IP>
      ansible_user: ubuntu
      ansible_ssh_private_key_file: /path/to/your-key.pem
  ```




# Run the Playbook:
```
ansible-playbook -i inventory/ec2.yml playbooks/playbook.yml

```


# Verify the Deployment:
Open a browser and navigate to http://<EC2_PUBLIC_IP>/index.php.
You should see a sample PHP page displaying PHP info and MySQL connection status.


# Challenges Faced

* SSH Connectivity: Ensuring the EC2 instance’s security group allows SSH and the correct key pair is used.
* MySQL Secure Installation: Automating the mysql_secure_installation process required careful handling of the root password and non-interactive commands.
* Ansible Idempotency: Ensuring tasks like package installation and service restarts are idempotent to avoid errors on re-runs.
* EC2 Resource Limits: Free-tier EC2 instances have limited resources, which can cause performance issues during deployment.
* Version Compatibility: Ensuring compatibility between Ubuntu, Apache, MySQL, and PHP versions.

# Possible Future Improvements
* Dynamic Inventory: Use Ansible’s AWS dynamic inventory to automatically discover EC2 instances.
* High Availability: Extend the playbook to deploy a load-balanced LAMP stack across multiple EC2 instances.
* CI/CD Integration: Integrate with tools like Jenkins or GitHub Actions to trigger deployments on code changes.
* Advanced Security: Add SSL/TLS support with Let’s Encrypt and configure a firewall (e.g., UFW).
* Monitoring: Integrate monitoring tools like Prometheus or CloudWatch to track server health.
* Containerization: Adapt the project to deploy the LAMP stack in Docker containers for portability.


