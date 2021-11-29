## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

DVWA-Project/diagrams/Week 12 Homework - Azure Resource Group.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible playbook file may be used to install only certain pieces of it, such as Filebeat.

  DVWA-Project/ansible/ansible-playbook.docx

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA (D*mn Vulnerable Web Application).

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
Load balancers protect servers from being overloaded, minimize server response time, and maximize throughput. A jump box is a secure computer that all admins first connect to before launching any administrative task or use as an origination point to connect to other servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name                 | Function | Private IP Address | Public IP Address | Operating System |
|----------------------|----------|--------------------|------------------ |------------------
| Jump Box Provisioner | Gateway  | 10.0.0.7           | 51.143.3.171      | Linux            |
| ELK                  | Logging  | 10.2.0.4           | 20.106.78.186     | Linux            |
| Web-1                | Computer | 10.0.0.9           | 20.69.103.226     | Linux            |
| Web-2                | Computer | 10.0.0.10          | 20.69.120.175     | Linux            |
| Load Balancer        | Computer | 10.0.0.10          | 20.112.95.85      | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

The Jump Box Provisioner, ELK, Web-1, Web-2, and Red Team Load Balancer can be accessed from the internet when the machines are started in Microsoft Azure. The public IP addresses for each machine when they are started are listed as followed: (Name, Public IP Address)
- Jump Box Provisioner, 51.143.3.171
- ELK, 20.106.78.168
- Web-1, 20.69.103.226 
- Web-2, 20.69.120.175
- Load Balancer, 20.112.95.85

Machines within the network can only be accessed by the Jump Box Provisioner.
- The Jump Box Provisioner IP address goes as follows: 52.183.18.67

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Addresses |
|---------------------|---------------------|----------------------|
| Jump Box            | Yes                 | 20.80.191.69         |
| Web-1               | No                  | 10.0.0.9             |
| Web-2               | No                  | 10.0.0.10            |
| Azure Load Balancer | Yes                 | 20.112.95.85         |  

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the feedback loop is accelerated at a faster rate, bugs are found sooner and not wait till the end, risk due to lack of sufficient knowledge is mitigated, the deployments are reliable, IT infrastructure is coordinated, and deployments are faster.

The playbook implements the following tasks:
- Install Python Docker Module
- Download and launch the Docker container
- Enable docker srvice

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(https://github.com/prush-ds/DVWA-Project/blob/main/diagrams/elk.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1
- Web 2

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. In case of network issues or interruptions in transmissions, Filebeat will remember where it left off when re-establishing a connection. If there is an ingestion issue with the output, Logstash or Elasticsearch, Filebeat will slow down the reading of files.
- Metricbeat takes the metrics and statistics that it collects and ships them to Elasticsearch or Logstash. Metricbeat helps monitor servers by collecting metrics from the system and services running on the ELK server. You’ll see cluster alerts that require your attention and a summary of the available monitoring metrics for Elasticsearch, Logstash, and Kibana. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml and metricbeat-playbook.yml file to roles.
- Update the Ansible playbook to run on a specific machine. Use the install-elk.yml file to specify install on the ELK server and the filebeat-config.yml to install Filebeat. 
- Run the playbook, and navigate to http://20.106.78.186:5601/app/kibana#/home

