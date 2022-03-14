# Automated-ELK-Stack-Deployment
The purpose of this project is to configure the deployment of an ELK stack server.
## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

![Network Diagram](https://github.com/msnee457/Automated-ELK-Stack-Deployment/blob/main/Diagrams/Project_1_Network_Diagram_ELK_Stack_Deployment.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the *yml* file may be used to install only certain pieces of it, such as Filebeat.

 [filebeat-playbook.yml](https://github.com/msnee457/Automated-ELK-Stack-Deployment/blob/main/Ansible/filebeat-playbook.yml.txt)
 
 [metricbeat-playbook.yml](https://github.com/msnee457/Automated-ELK-Stack-Deployment/blob/main/Ansible/metricbeat-playbook.yml.txt)

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
| Jump Box      | Gateway  | Public: 52.150.22.109/Private:10.0.0.4 | Linux            |
| Web-1         | Server   | Private: 10.0.0.5                      | Linux            |
| Web-2         | Server   | Private: 10.0.0.6                      | Linux            |
| Elk Server VM | Server   | Public: 13.64.172.95/Private:10.1.0.6  | Linux            |

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
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Ansible allows applications to be deployed across machines identically using an ansible playbook file. 

The playbook implements the following tasks:

#### Installing the following modules:

    - name: Install docker.io
      apt:
        update_cache: yes
        force_apt_get: yes
        name: docker.io
        state: present

    - name: Install python3-pip
      apt:
        force_apt_get: yes
        name: python3-pip
        state: present

    - name: Install Docker module
      pip:
        name: docker
        state: present

#### Increasing system memory:

    - name: Use more memory
      sysctl:
        name: vm.max_map_count
        value: "262144"
        state: present
        reload: yes

#### Launching the Docker container:

    - name: download and launch a docker elk container
      docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        # Please list the ports that ELK runs on
        published_ports:
          -  5601:5601
          -  9200:9200
          -  5044:5044
          
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker PS](https://github.com/msnee457/Automated-ELK-Stack-Deployment/blob/main/Images/ELK_Docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

•	Web-1: 10.0.0.5

•	Web-2: 10.0.0.6

We have installed the following Beats on these machines:

•	We have successfully installed Filebeat.

•	We have successfully installed Metricbeat.

These Beats allow us to collect the following information from each machine:

Filebeat collects data from log files that it generates and organizes in the system. Changes that have occurred in these files are logged and sent to Logstash and Elasticsearch. 

Metricbeat collects metrics and statistics from the system and various services that run on the system and sends them to Logstash and Elasticsearch.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:

For Filebeat:

Run `curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/filebeat-config.yml`

Edit “filebeat-config.yml”

Scroll to “output.elasticsearch” and replace the IP address with the private IP of ELK Server VM

Scroll to “setup.kibana” and replace IP address with the private IP of ELK Server VM

Copy /etc/ansible/filbeat-config.yml to /etc/ansible/files/filebeat-config.yml


- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.
_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
