## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

**Note**: The following image link needs to be updated. Replace `diagram_filename.png` with the name of your diagram image file.  

(C:\Users\jnewm\Project-1-Elk-Stack\Diagrams)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  The Following ansible-playbooks are needed to create, install or modify the relevant variables.

  My Ansible playbook -
  My Elk playbook -
  My Filebeat playbook -
  My Metricbeat playbook -

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. With the Load balancer in place, it is assisting with the availability of the network, itself a part of the availabily aspect of the CIA triad and additionally layer 4 of OSI.

The benefits to utilising a jump box is that we have one point of origination point to connect to for when we are either performing administrative tasks or additionally, preparing to connect to other environments that we may not trust entirely. As we use the jumpbox as our first point to ssh into, it operaties as a 'secure admin workstation' or SAW, ensuring that our local machines are removed when moving throughout this network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

Filebeat - Filebeat helps to forward and centralise your log data. When it is installed on your servers, it helps monitoring the log events, specific logs that you select and moves them to either Elasticsearch or Logstash where they are indexed.

Metricbeat - Metricbeat is similiar but in its use of metrics and statistics before shipping them to the output of Elasticsearch or Logstash. Metricbeat can assist in collecting the metrics from systems and services that you have running. 

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|--------------------|------------|------------------|
| Jump Box | Gateway            | 10.0.0.4   | Linux            |
| WEB-1    |Web server - Docker | 10.0.0.5   | Linux            |
| Web-2    |Web server - Docker | 10.0.0.6   | Linux            |
| Elk-VM-1 |ELK stack           | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- My own personal IP address.

Machines within the network can only be accessed by SSH.

Regarding the ELK-server, it is accessible via ssh from the Jump box machine utilising ansible. Additionally, there is web access via my personal IP address.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|------------------------------------------------------|
| Jump Box | Yes                 | My personal IP                                       |
| WEB-1    | No                  |   10.0.0.4 - Jumpbox   40.127.86.196 - Load Balancer |
| Web-2    | No                  |   10.0.0.4 - Jumpbox   40.127.86.196 - Load Balancer |
| ELK-VM-1 | No                  |   10.0.0.4 - Jumpbox   My personal IP                |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because ansible is relatively easy to utilise via palybooks, allowing us to install and modify the systems we used in a streamlined manner. It also provides a template that if changes were ever made, they are simple to deploy as opposed to starting entirely from scratch.


The playbook implements the following tasks:
- Increased VM memory 
- Installed Docker.io and Python3-pip
- Downloaded the Docker container and established ports.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

**Note**: The following image link needs to be updated. Replace `docker_ps_output.png` with the name of your screenshot image file.  


(C:\Users\jnewm\Project-1-Elk-Stack\Ansible)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
WEB-1 - (10.0.0.5)
Web-2   (10.0.0.6)

We have installed the following Beats on these machines:
- Filebeat
- MetricBeat

These Beats allow us to collect the following information from each machine:
Filebeat - Filebeat helps to forward and centralise your log data. When it is installed on your servers, it helps monitoring the log events, specific logs that you select and moves them to either Elasticsearch or Logstash where they are indexed.

Metricbeat - Metricbeat is similiar but in its use of metrics and statistics before shipping them to the output of Elasticsearch or Logstash. Metricbeat can assist in collecting the metrics from systems and services that you have running. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the config files the ansible node location, for my files it was originally /etc/ansible/roles.
- Update the configuration file to include the private ip of the ELK server, specifically the ElasticSearch and Kibana    sections of the config file.
- Run the playbook, and navigate to [ELK.VM.EXTERNAL.IP]:5601/app/kibana  to check that the installation worked as expected.


-The Playbook files which I utilised were 
  - elk-playbook.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml
  - They were copied within my ansible container /etc/ansible/roles

  - If you update the configuration files it will allow you to specify where to install, whether it be ELK or Filebeat

- _Which URL do you navigate to in order to check that the ELK server is running?
[ELK.VM.EXTERNAL.IP]:5601/app/kibana

While Utilising Kibana, we were able to analyse and study a variety of information regarding the metrics and traffic that our Web VM's were recieiving. In the top right corner is a dropdown that allows you manipulate what timeframe of data that you would like to analyse and the dashboards present all the variatals to you in an easy to process manner.

In the same data dashboard, it presents visitors as well as where they are located geographically, what sort of data and information is being utilised, what file types and what errors are recieved.

Additionally, we were able to simulate an investigation for if there are multiple ssh failed log in attempts and CPU usage, as well as using Kibana to displau this data in a form that would be presentable in such a situation where a real life attack was occuring.
