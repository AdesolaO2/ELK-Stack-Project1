## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_Network Diagramming.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

- _TODO: Enter the playbook file._

---
  - name: Install Filebeat
    hosts: webservers
    become: true
    tasks:
      # Download.deb
      - name: Download.filebeat.deb
        command: curl https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb -O

      # Install filebeat
      - name: Download filebeat.deb
        command: dpkg -i filebeat-7.4.0-amd64.deb

      # Copy filebeat config
      - name: Copy config files
        copy:
          src: /etc/ansible/files/Filebeat-config.yml
          dest: /etc/filebeat/filebeat.yml

      # Setup Filebeat
      - name: Allow Modules System
        command: filebeat modules enable system

      # Filebeat setup
      - name: Filebeat setup
        command: filebeat setup

      # Filebeat -e
      - name: Filebeat -e
        command: sudo service filebeat start

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
- _TODO: What aspect of security do load balancers protect? The load balancer is crated to distribute and optimize traffic or load among the virtual machines.  It serves as an extra layer of security while protecting apllications from threats.  What is the advantage of a jump box? Using the jump box as a gateway to other virtual machines will force traffic through a single node. This will allow for a more secure connection and easy way to manage connections between machines.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for? Filebeat is installed as an agent on the servers to monitor system log files to collect data while forwarding log events to elasticsearch.
- _TODO: What does Metricbeat record? Metricbeat take the metric and statistics that it collects and forwards the information to the output that is specied, in this care Elasticsearch/Kibana.  This will help to monitor servers.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
                                                                      
| Jumpbox | Gateway | 10.0.0.4 | Linux |   |
|---------|---------|----------|-------|---|
| Web-1   | Server  | 10.0.0.5 | Linux |   |
| Web-1   | Server  | 10.0.0.6 | Linux |   |
| ELK-VM  | Server  | 10.1.0.4 | Linux |   |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses 52.170.192.207

Machines within the network can only be accessed by Jump-Box-Provisioner.
- _TODO: Which machine did you allow to access your ELK VM? Jump-Box-Provisioner  What was its IP address? 52.170.192.207



A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------| 
| Jump Box | Yes/No       | 10.0.0.4    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible? Using Ansible for automating and configuring allows for daily task to be executed or deplyed on time, effortlessly and in order.  This will allow administrators to focus other other complex task at the same time being highly productive.   

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Create a new vNet...
- Create a Peer Network
- Create a new VM
- Download and configure a container
- Launch and expose the container
- Implement identity and access management...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/Adesola Olasina – Project 1 Images.odt)

### Target Machines & Beats
This ELK server is configured to monitor the following machines: 
- _TODO: List the IP addresses of the machines you are monitoring_
- Web-1: 10.0.0.5
- Web-2: 10.0.0.6

	
We have installed the following Beats on these machines:

- _TODO: Specify which Beats you successfully installed_Filebeat-7.4.0-amd/64.deb on the DVMA container

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
The Filebeat-7.4.0-amd/64.deb is used to forward and centralize log data.  Installed as an agent on the servers to monitor system log files to collect data while forwarding log events to elasticsearch.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? filebeat-playbook.yml Where do you copy it?_ 

- _Which file do you update to make Ansible run the playbook on a specific machine? Host file (Webservers and Elk Server)ls How do I specify which machine to install the ELK server on versus which to install Filebeat on?_Use install-elk.yml to specify that the elk server will be downloaded and launched on a docker elk container (sebp/elk:761).  Use filebeat-playbook.yml to specify that the filebeat will be downloaded and installed on the host:servers machines.

- _Which URL do you navigate to in order to check that the ELK server is running? http://104.43.196.174:5601/app/kibana#/home/tutorial/systemLogs 

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

-ansible-playbook filename.yml

- nano filename.yml (to update file)
