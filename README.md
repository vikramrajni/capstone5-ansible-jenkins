This project demonstrates how to integrate Jenkins and Ansible to automate the configuration of AWS EC2 instances.

### Objectives

- Create and configure a dedicated Jenkins server.
- Create and configure a dedicated Ansible Control Node server
  This server was created in Digital Ocean
- Develop an Ansible playbook to configure two EC2 Managed Nodes.
- Store SSH private keys securely in Jenkins Credentials to login to Ansible Server.
- Execute the Ansible playbook remotely through a Jenkins CI/CD pipeline.

### Jenkins Pipeline Workflow

1. Connect to the Ansible Control Node server.
2. Transfer the Ansible playbook, inventory_aws_ec2.yaml and ansible.cfg to the Ansible Control Node.
3. Transfer the SSH key required to access the Managed Ec2 Nodes. 
    Note:The EC2 servers' SSH key is saved as a credential in Jenkins.
4. Install Ansible, Python 3, and Boto3 on the Ansible Control Node.
5. Execute the Ansible playbook from the Control Node to configure the two EC2 Managed Nodes.
   The playbook will install docker and docker compose on both EC2 instances



