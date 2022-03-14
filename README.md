# Automated-ELK-Stack-Deployment
The purpose of this project is to configure the deployment of an ELK stack server.
## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
(Diagrams/Project 1 Network Diagram ELK Stack Deployment.png)
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.
  - _TODO: Enter the playbook file._
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build
### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly functional, in addition to restricting traffic to the network.

What aspect of security do load balancers protect? 

  •	Load balancers protect the network from experiencing downtime due to heavy network traffic and potential Denial of Service attacks. Additionally, load balancers distribute traffic more evenly across network servers. 

What is the advantage of a jump box?

  •	The advantage of a jump box is that it is the only machine on the network exposed to the public internet, making it a gateway for the network. All other machines and servers are not exposed and therefore, less vulnerable to attack. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

What does Filebeat watch for?

  •	Filebeat watches for changes in logfiles on the system. 

What does Metricbeat record?

  •	Metricbeat records statistics and metric data on the system. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.
| Name          | Function | IP Address                            | Operating System |
|---------------|----------|---------------------------------------|------------------|
| Jump Box      | Gateway  | Public:52.150.22.109/Private:10.0.0.4 | Linux            |
| Web-1         | Server   | Private:10.0.0.5                      | Linux            |
| Web-2         | Server   | Private:10.0.0.6                      | Linux            |
| Elk Server VM | Server   | Public:13.64.172.95/Private:10.1.0.6  | Linux            |
### Access Policies
The machines on the internal network are not exposed to the public Internet. 
Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

  •	47.152.190.52 (Workstation IP Address)

Machines within the network can only be accessed by the Jump Box Provisioner VM.

Which machine did you allow to access your ELK VM? What was its IP address?

  •	The Jump Box Provisioner is allowed to access the ELK Server VM using the IP address 10.0.0.4. The workstation computer is also allowed access to the ELK Server VM through TCP Port 5601. 

A summary of the access policies in place can be found in the table below.
| Name          | Publicly Accessible | Allowed IP Addresses                            |
|---------------|---------------------|-------------------------------------------------|
| Jump Box      | No                  | Workstation IP: 47.152.190.52 through SSH       |
| Web-1         | No                  | Jump Box IP: 10.0.0.4 through SSH               |
| Web-2         | No                  | Jump Box IP: 10.0.0.4 through SSH               |
| Elk Server VM | No                  | Workstation IP: 47.152.190.52 through Port 5601 |
| Load Balancer | No                  | Workstation IP: 10.0.0.4 through Port 80        |

### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
### Target Machines & Beats
This ELK server is configured to monitor the following machines:

  •	Web-1: 10.0.0.5

  •	Web-2: 10.0.0.6
We have installed the following Beats on these machines:

  •	We have successfully installed Filebeat.

  •	We have successfully installed Metricbeat.
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.
_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
