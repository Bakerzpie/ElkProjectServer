## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._ 
  - install-elk.yml 
  - filebeat-playbook.yml
  - metricbeat.config
  - pentest.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. 
- What aspect of security do load balancers protect? Load balancers ensure that if a server goes down, or needs to be updated, services can still continue being available. 
- What is the advantage of a jump box? The advantage of using a jump box is that only it can access the Virutal networks via ssh.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the filesystem and system logs.
- Filebeat monitors the log files or locations specified, it collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat is an easy to use, efficient and reliable metric shipper for monitoring your system and the processes running on it. 

The configuration details of each machine may be found below.
[Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables)

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.6   | Linux            |
|ElkServer |  Config  | 10.2.0.4   | Linux            |
| Web-1    |   DVWA   | 10.1.0.4   | Linux            |
| Web-2    |   DVWA   | 10.1.0.5   | Linux            |
| Web-3    |   DVWA   | 10.1.0.7   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 49.198.203.101 - my local ip address
- 5061 Kibana port

Machines within the network can only be accessed by Jump-Box-Provisioner.
- The Jump-BoxVM ansible docker container was allowed to access the ElkVM with Jumpbox IP of :10.1.0.6

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes - SSH only      | 10.1.0.6, MyPublicIP |
|ElkServer | No                  | HTTP(5601) MyIP only |
| Web-*    | No                  | HTTP(80) MyIP Only   |
| Load Bal | No                  |HTTP(80) -TrafficToWeb|       

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because automation provides efficiency, and less chance of a human error or mess up.

The playbook implements the following tasks:

- Install Docker.io
- Install Python3-pip
- Configures Docker to use more memory
- Install ELK container
- Enables Docker to run at start

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[](sudodockerps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines: Web-1, Web-2, and Web-3
- Web-1 IP:10.1.0.4
- Web-2 IP:10.1.0.5
- Web-3 IP:10.1.0.7

We have installed the following Beats on these machines: 
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat detects changes to the file system and collects log files and events, ie 'Apache logs'.
- Metricbeat detects changes in system metrics such as CPU or memory then shows the docker performance data in either Logstash or Elasticsearch.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook(.yml) file to the ansible directory.
- Update the host file to include Webservers and ELK
- Run the playbook, and navigate to the kibana page 'http://[Your Public Ip]:5601/app/kibana' to check that the installation worked as expected.

- Which file is the playbook? Where do you copy it? install-elk.yml is copied to '/etc/ansible'
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? You modify the ansible.cfg, install-elk.yml, and hosts as directed. 
- Which URL do you navigate to in order to check that the ELK server is running? 'http://[YourPublicIp]:5601/app/kibana'

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._