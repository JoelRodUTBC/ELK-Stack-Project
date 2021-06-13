-## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)
https://drive.google.com/file/d/1Yql_cI1MhETD_kdUgivc1XBSut3sKAw4/view?usp=sharing
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._
	- Ansible/filebeat-playbook.yml
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
	- Load balancers monitor the flow of traffic in a network, so if a server were to go down, the load balancer will redirect the traffic between all the live servers; the advantage of a Jump-Box is that this is the only machine connected to the internet, while the rest of the machines remain hidden inside the network.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_
	- The filebeat collects log events and monitors the files and sent to Elasticsearch and/or Logstash for indexing.
- _TODO: What does Metricbeat record?_
	- Metricbeat records metrics from multiple services ie. Apache, nginx, MySQL, MongoDB, etc.
The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
|  ELK VM  | DockerVM | 10.1.0.4   | Linux            |
|  Web-1   | DockerVM | 10.0.0.6   | Linux            |
|  Web-2   | DockerVM | 10.0.0.8   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
	- 52.149.181.76
- _TODO: Add whitelisted IP addresses_
	- 10.0.0.6
	- 10.0.0.8
	- 10.1.0.4
Machines within the network can only be accessed by Jump-Box Provisioner.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?
	- Only the Jump-Box VM ansible container is allowed access into the ELK VM. As for the IP address of the ELK VM, it is listed as 10.1.0.4.
A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |   No                | 10.0.0.6 10.0.0.8    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
	- Ansible allows easier deployment for different applications.
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
	- The first step is creating a new Virtual Network in the same Resource Group that has been in use.
	- Both Virtual Networks are then peered together to establish a connection between the two of them.
	- Log into the Jump-Box Provisioner and collect the public key from the ansible container to create a connection to the ELK Virtual Machine.
	- Once the connection is established, the created Virtual Machine is added to the hosts file in order to create an ansible playbook.
	- A playbook, written in yaml, is created to install services such as docker.io, python3-pip, & docker.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
	- 10.0.0.6
	- 10.0.0.8
	- 10.1.0.4
We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
	- I was successfully able to install filebeat system logs.
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
	- Filebeats collects different kinds of data such as system logs and metric beats collects information from running servers and both beats send them to the ELK stack.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook.yml file to the ansible container.
- Update the ansible.cfg file to include IP addresses of Web-1 and Web-2.
- Run the playbook, and navigate to container to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
	- Filebeat-playbook.yml is my playbook that I created.  
	- The file is copied to the Jump-Box.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
	- The playbook file itself will need to be updated.
	- Adding the ELK VM's IP address to the ansible.cfg.
- _Which URL do you navigate to in order to check that the ELK server is running?
	- http://137.135.18.47:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._