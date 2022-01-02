**Configuring The Elk Stack**

**1. Add A New Virtual Network To The Red-Team Resource Group In A Different Region**

1.1 Name This Network Elk-Net

**2. Add A New Peering To Allow Elk-Net and Red-Team-Net To Communicate**

2.1 Select Elk-Net > Peerings > Add A New Peering

2.2 Name The Peering Elk-Red and Name the Reverse Red-Elk

2.3 Add Red-Team-Net as the Virtual Network That You Are Trying To Reach

**3. Configure A New VM**

3.1 Name This New VM Elk-Server

3.2 Select 4GB or 8GB of RAM

3.3 Place This Machine In The Red-Team Resource Group

3.4 Configure The Back-End Login Using The SSH Public Key Of The Ansible Container

3.5 Drop Into The Ansible Container

Commands To Drop Into Container:

1. sudo docker ps

2. sudo docker container list -a (Lists Containers)

3. sudo docker start busy_mayer (Starts busy_mayer Container)

4. sudo docker attach busy_mayer (Drops Into busy_mayer Container)

3.6 Verify That You Can Connect To The Elk-Server VM From The Ansible Container

Command: ssh RedAdmin@<Elk-Server IP>

**4. Edit The Ansible Hosts File and Add The Elk-Server VM**

Command: nano /etc/ansible/hosts

Enter The Following Into The Hosts File:

[Elk]

10.2.0.4 ansible_python_interpreter=/usr/share/bin

**5. Configure The Elk Server Using The Elk Server Playbook**

Playbook: install-elk.yml

Command: ansible-playbook install-elk.yml

**6. Verify That The Elk Container Is Running**

6.1 Log Into The Back End Of The Elk Server VM

Command: ssh RedAdmin@<Elk-Server IP>

6.2 Verify That The Elk Container Is Running Correctly

Command: sudo docker ps

**7. Allow Your Host Machine To Access Elk-Server Over HTTP**

7.1 Add An Inbound Security Rule To Elk-Net

Source IP: <Host Machine Public IP>

Destination Port: Custom 5601 HTTP

**8. Verify That You Can Access The Elk-Server Over HTTP**

8.1 Navigate To http://[Elk-Server External IP]:5601/app/kibana

**9. Install Filebeat **

9.1 Download The Filebeat Configuration File

Command: curl https://github.com/SundownRider/Elk-Stack-Project/blob/main/Ansible/filebeat-configuration.yml

9.2 Edit The Filebeat Configuration File

9.2.1 Scroll To Line 1106 and Replace The IP With Your Elk-Server IP (Elasticsearch)

Example: hosts: ["10.2.0.4:9200"]

9.2.2 Scroll To Line 1806 and Replace The IP With Your Elk-Server IP (Kibana)

Example: host: "10.2.0.4:5601"

9.3 Run The Filebeat Playbook

Command: ansible-playbook filebeat-playbook.yml

9.4 Verify The Installation

9.4.1 Kibana Website > Logs > System Logs > Module Status > Select Check Data

**10. Install Metricbeat**

10.1 Download The Metricbeat Configuration File

Command: curl https://github.com/SundownRider/Elk-Stack-Project/blob/main/Ansible/metricbeat-configuration.yml

10.2 Edit The Metricbeat Configuration File

10.2.1 Scroll To Line 1106 and Replace The IP With Your Elk-Server IP (Elasticsearch)

Example: hosts: ["10.2.0.4:9200"]

10.2.2 Scroll To Line 1806 and Replace The IP With Your Elk-Server IP (Kibana)

Example: host: "10.2.0.4:5601"

10.3 Run The Metricbeat Playbook

Command: ansible-playbook metricbeat-playbook.yml

10.4 Verify The Installation

10.4.1 Kibana Website > Metrics > System Metrics > Module Status > Select Check Data
