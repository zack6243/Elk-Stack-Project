# Elk-Stack-Project
Elk Stack Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/83610301/146652133-d72287d4-bbec-460b-854c-9f4199c5f111.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above or, alternatively, select files may be used to install only certain pieces of it such as Filebeat. Ex:

  ![Filebeat-Playbook.yml](https://github.com/zack6243/Elk-Stack-Project/blob/main/Ansible/filebeat-playbook.yml)
  
  ![Filebeat-Config.yml](https://github.com/zack6243/Elk-Stack-Project/blob/main/Ansible/filebeat-config.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting access to the internal network.
Load balancers protect the availability aspect of security by ensuring that network traffic is distributed equally between two or more webservers so as not to overload a single server with more traffic than it can handle. Also, creating a jumpbox can be adventageous because one advantage of this system is the ability to effectively manage multiple webservers and/or programs individually and effeciently by making them accessible through a single gateway.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the server's logs and the system metrics.
- _Filebeat: Filebeat monitors the system logs and sends the output to a program that makes it easy to track, such as elasticsearch._
- _Metricbeat: Metricbeat records system statistics and metrics. It also sends them to a program like elasticsearch._

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web 1    | Webserver| 10.0.0.5   | Linux            |
| Web 2    | Webserver| 10.0.0.6   | Linux            |
|Elk-Server|Monitoring| 10.0.2.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _Elk-Server Public IP: 74.192.25.186_

Machines within the network can only be accessed by SSH.
- _The ansible machine which was hosted in a container on Jump Box is allowed to access the Elk-Server on the back end._

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses              |
|----------|---------------------|-----------------------------------|
| Jump Box | No                  | 74.192.25.186                     |
| Web 1    | No                  | 74.192.25.186 or 10.0.0.4         |
| Web 2    | No                  | 74.192.25.186 or 10.0.0.4         |
|Elk-Server| Yes                 | 74.192.25.186 or 10.0.0.4         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it minimizes the risk that the machines would be misconfigured or set up incorrectly.

The playbook implements the following tasks:
- _Install the Docker.io package_
- _Install Python3_
- _Install the Docker module using Python3_
- _Extend the amount of memory allocated to Docker_
- _Download and launch the Elk container using Docker_

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/83610301/147888158-1b3d25bf-d763-49ff-8b27-ddc5facffd0f.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _Web-1: 10.0.0.5_
- _Web-2: 10.0.0.6_

We have installed the following Beats on these machines:
- _Filebeat_
- _Metricbeat_

These Beats allow us to collect the following information from each machine:
- _Filebeat collects system logs and monitors network activity. These logs can be used to locate or detect unauthorized access or suspicious activity._
- _Metricbeat collects system metrics which can identify performace issues on the network or issues with the server._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- _Copy the elk-ansible.yml file to the ansible directory._
- _Update the /etc/ansible/hosts file to include the IP addresses of the webservers that you would like to install ELK on and the IP address of the ELK virtual machine._
- _Run the playbook, and navigate to http://[Elk-Server External IP]:5601/app/kibana to ensure that the installation was successful._

For detailed steps on the commands used and how to set this up, reference this document: https://github.com/zack6243/Elk-Stack-Project/blob/main/ConfigurationWriteUp.md
