## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(https://drive.google.com/file/d/1Lk9qvZQi_UQlH8qb8PhmTyqGRf8DGZ4m/view?usp=sharing)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Network Diagram file may be used to install only certain pieces of it, such as Filebeat.

  - command: ansible-playbook install-elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available and reliable by sending requests only to servers that are online, in addition to restricting unauthorized access to the network.
- Load balancers protect networks from DDoS attacks by shifting traffic from the corporate server to the public cloud provider. On the other hand, advantages of a jumpbox is that you can update one system and it will update other systems connected with the jumpbox, reducing load time.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the docker conatiner and system logs.
- Filebeat monitors the system log files or locations that you specify and collects log events.
- In similar fashion, Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as Apache, MySQL and many more.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| BlueJump | Gateway  | 10.0.0.4   | Linux            |
| Web-1    |  Server  | 10.0.0.7   | Linux            |
| Web-2    |  Server  | 10.0.0.8   | Linux            |
| Web-3    |  Server  | 10.0.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 76.98.162.133

Machines within the network can only be accessed by ssh.
- In order to access the ELK VM (Web-4) we need to ssh from our jumpbox ansible i.e. ssh BlueAdmin@10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |          No         | 10.0.0.7 10.0.0.8/5  |
|  Web-1   |          No         |       10.0.0.4       |
|  Web-2   |          No         |       10.0.0.4       |
|  Web-3   |          No         |       10.0.0.4       |
|Web-4(Elk)|          No         |       10.0.0.4       |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because there will be more time to focus efforts elsewhere. Utilizing ansible makes it easier to create computer software and processes.

The playbook implements the following tasks:
- Install docker.io 
- Install python3-pip
- Install docker python module
- Download web container from cybersecurity/dvwa
- Enable Docker service
- Other playbooks will install Filebeat and metricbeats

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://dochub.com/rdesakhamphou/orO7lgeVLJ8q88bRjMP2p5/screen-shot-2020-08-29-at-8-40-30-pm-png?dt=o58C7HYF1taszbri-evd

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.7 10.0.0.8 10.0.0.5

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeat will collect systemlog files such as audit logs while Metricbeat will collect data from specific services such as MySQL, if we were to install more services onto our machines.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to the ansible directory.
- Update the ansible hosts file to include Elk servers and web servers.
- Run the playbook, and navigate to elk-vm-public-ip:5601 (Kibana) to check that the installation worked as expected.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
Commands
- ssh BlueAdmin@jumpboxvmpublicip (BlueAdmin@13.68.155.127)
- sudo docker ps
- sudo docker start sleepy_snyder (ansible container)
- sudo docker attach sleepy_snyder
- navigate to find where the playbook for the Elk installation is located
- cd /etc/ansible/
- ls to ensure the playbook is in the ansible directory
- run ansible-playbook install-elk.yml
- ssh to elk vm to ensure connection is made and elk container is working
- run ssh BlueAdmin@10.1.0.4 (Elk VM IP)
- once in the elk VM you can run docker ps to see the elk container
- verify the jumpbox public ip and insert into web browser http://13.64.98.182:5601 to navigate to kibana and check logs the elkstack vm is monitoring for the 3 VMs under the jumpbox