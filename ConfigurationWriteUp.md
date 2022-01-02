**Configuring The Elk Stack**

**1. Add A New Virtual Network To The Red-Team Resource Group In A Different Region**

**-** Name This Network Elk-Net

**2. Add A New Peering To Allow Elk-Net and Red-Team-Net To Communicate**

**-** Select Elk-Net > Peerings > Add A New Peering

**-** Name The Peering Elk-Red and Name the Reverse Red-Elk

**-** Add Red-Team-Net as the Virtual Network That You Are Trying To Reach

**3. Configure A New VM**

**-** Name This New VM Elk-Server

**-** Select 4GB or 8GB of RAM

**-** Place This Machine In The Red-Team Resource Group

**-** Configure The Back-End Login Using The SSH Public Key Of The Ansible Container

**-** Drop Into The Ansible Container

_Commands To Drop Into Container:_

**1.** sudo docker ps

**2.** sudo docker container list -a (Lists Containers)

**3.** sudo docker start busy_mayer (Starts busy_mayer Container)

**4.** sudo docker attach busy_mayer (Drops Into busy_mayer Container)

**-** Verify That You Can Connect To The Elk-Server VM From The Ansible Container

_Command: ssh RedAdmin@<Elk-Server IP>_

**4. Edit The Ansible Hosts File and Add The Elk-Server VM**

_Command: nano /etc/ansible/hosts_

Enter The Following Into The Hosts File:

[Elk]

10.2.0.4 ansible_python_interpreter=/usr/share/bin

**5. Configure The Elk Server Using The Elk Server Playbook**

Playbook: install-elk.yml

_Command: ansible-playbook install-elk.yml_

**6. Verify That The Elk Container Is Running**

**-** Log Into The Back End Of The Elk Server VM

_Command: ssh RedAdmin@<Elk-Server IP>_

**-** Verify That The Elk Container Is Running Correctly

Command: sudo docker ps

**7. Allow Your Host Machine To Access Elk-Server Over HTTP**

**-** Add An Inbound Security Rule To Elk-Net

Source IP: <Host Machine Public IP>

Destination Port: Custom 5601 HTTP

**8. Verify That You Can Access The Elk-Server Over HTTP**

**-** Navigate To http://[Elk-Server External IP]:5601/app/kibana

**9. Install Filebeat**

**-** Download The Filebeat Configuration File

_Command: curl https://github.com/zack6243/Elk-Stack-Project/blob/main/Ansible/filebeat-config.yml_

**-** Edit The Filebeat Configuration File

**-** Scroll To Line 1106 and Replace The IP With Your Elk-Server IP (Elasticsearch)

Example: hosts: ["10.2.0.4:9200"]

**-** Scroll To Line 1806 and Replace The IP With Your Elk-Server IP (Kibana)

Example: host: "10.2.0.4:5601"

**-** Run The Filebeat Playbook

_Command: ansible-playbook filebeat-playbook.yml_

**-** Verify The Installation

**-** Kibana Website > Logs > System Logs > Module Status > Select Check Data

**10. Install Metricbeat**

**-** Download The Metricbeat Configuration File

_Command: curl https://github.com/SundownRider/Elk-Stack-Project/blob/main/Ansible/metricbeat-configuration.yml_

**-** Edit The Metricbeat Configuration File

**-** Scroll To Line 1106 and Replace The IP With Your Elk-Server IP (Elasticsearch)

Example: hosts: ["10.2.0.4:9200"]

**-** Scroll To Line 1806 and Replace The IP With Your Elk-Server IP (Kibana)

Example: host: "10.2.0.4:5601"

**-** Run The Metricbeat Playbook

_Command: ansible-playbook metricbeat-playbook.yml_

**-** Verify The Installation

**-** Kibana Website > Metrics > System Metrics > Module Status > Select Check Data
