# CLoud-Monitoring
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/gedanigat/CLoud-Monitoring/blob/main/Diagram/ELK-Network%20Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible playbook file may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml
  - filebeat-config.yml
 
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


 Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- A load balancer can add an additional layers of Security and protects a website from hackers and emerging threats. 
- A jump-box is used as a gateway to Virtual Machines, prevents Virtual Machines exposure to the public.By using the network Security group, we can restrict the ip addresses to communicate with the jump-box.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system metrics.
- Filebeat helps generate and organize log files to send to Logstash and Elasticsearch. Specifically, it logs information about the file system, including which files have changed and when.
- Metricbeat is an easy-to-use, efficient and reliable metric shipper for monitoring your system and the processes running on it.

The configuration details of each machine may be found below.


| Name     	| Function        	| IP Address 	| Operating System 	|
|----------	|-----------------	|------------	|------------------	|
| Jump-Box 	| Gateway         	| 10.0.0.6   	| Linux            	|
| Web-1    	| Virtual Machine 	| 10.0.0.10  	| Linux            	|
| Web-2    	| Virtual Machine 	| 10.0.0.11  	| Linux            	|
| ELK-VM   	| Server          	| 10.1.0.4   	| Linux            	|

 Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
73.158.88.4 (my ip address)

Machines within the network can only be accessed by Jump-Box-Provisioner.

- The jump-box with an IP address of 40.76.66.241 have access to the Elk-VM.

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed Ip Addresses |
|---------------|---------------------|----------------------|
| Jump-box      | Yes                 | 73.158.88.2          |
| Web-1         | No                  | 10.0.0.6             |
| Web-2         | No                  | 10.0.0.6             |
| Elk-VM Server | No                  | 10.0.0.6             |

 Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The configuration takes place using YAML Playbooks. It is the best alternative for configuration management/automation.

The playbook implements the following tasks based on the procedures below:
- First, SSH into the Jump-Box-Provisioner (ssh gedanig@40.76.66.241)
- Start/Attached to the ansible docker (sudo docker start youthful_lederberg)/(sudo docker attach Youthful_lederberg)
- Accessed to /etc/ansible/roles directory and created the ELK playbook (Elkinstall.yml)

  Elk playbook does: apt install docker, apt install python3-pip, pip install docker module, increases VM memory to 262144, download and launch docker elk container with set of port mapping, enable the docker service on boot.
- Ran the Elkinstall.yml in that same directory
- Lastly, I SSH into the ELK-VM to verify the server is up and running.The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/gedanigat/CLoud-Monitoring/blob/main/Diagram/elk%20docker-ps.png
https://github.com/gedanigat/CLoud-Monitoring/blob/main/Diagram/ELK_VM%20Docker-ps.png

  Target Machines & Beats

This ELK server is configured to monitor the following machines:
- Web-1 : 10.0.0.10
- Web-2 : 10.0.0.11

We have installed the following Beats on these machines:

- https://github.com/gedanigat/CLoud-Monitoring/blob/main/Diagram/Filebeat%20Module%20Status.png
- https://github.com/gedanigat/CLoud-Monitoring/blob/main/Diagram/Metricbeat%20Module%20Status.png

These Beats allow us to collect the following information from each machine:

- Filebeat is used to collect log files from specific files on remote machines.Files that are generated by Apache, Microsoft Azure tools, the Nginx web server, and MySQl databases are some of the examples of Filebeat.

-Metricbeat collects machine metrics.It is a measurement to tell analysts how healthy the machine is. CPU usage/Uptime is among the tasks of metricbeat.

 Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

 Filebeat

- Copy the filebeat-config.yml file to /etc/ansible/files.
- Update the filebeat-config.yml file to include the private IP lines in 1106 and 1806.
- Run the playbook, and navigate to http://52.175.215.82(ELKVM IP):5601 to check that the installation worked as expected.

 Metricbeat

- Copy the metricbeat-configuration.yml file to /etc/ansible/files.
- Update the metricbeat-configuration.yml file to include the ELK private IP in lines 62 and 96.
- Run the playbook, and navigate to http://52.175.215.82(ELKVM IP):5601 to check that the installation worked as expected.

 Answer the following questions to fill in the blanks:_
- Which file is the playbook? filebeat-config.yml
- Where do you copy it? /etc/ansible/roles
- Which file do you update to make Ansible run the playbook on a specific machine? IP address of the Virtual Machines.
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? I have two groups on the host file: Web servers which I installed the filebeat to and ELK group in which I added the ELK server IP address and installed Elk to.
- _Which URL do you navigate to in order to check that the ELK server is running?
    http://52.175.215.82(ELKVM IP):5601
    
 -Inorder to create the filbeat-playbook.yml file, use the following command:
   Nano filebeat-playbook.yml.
Commands to install and download all the necessary fils are in the YML file as indicated below:![image](https://user-images.githubusercontent.com/95734193/145503678-252b4943-4f52-4810-aa7b-02dbc7f5159d.png)
