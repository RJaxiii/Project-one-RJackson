The files in this repository were used to configure the network depicted below.
Update the path with the name of your diagram](Images/diagram_filename.png)
https://github.com/RJaxiii/Project-one-RJackson/tree/main/Project%201%20Diagrams
![image](https://user-images.githubusercontent.com/85850505/122659226-70c27580-d13b-11eb-8036-1e521896b5dd.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  -  Enter the playbook file._
---
- name: Configure Elk VM with Docker
  hosts: elk
  remote_user: sysadmin
  become: true
  tasks:
    # Use apt module
    - name: Install docker.io
      apt:
        update_cache: yes
        name: docker.io
        state: present
      # Use apt module
    - name: Install pip3
      apt:
        force_apt_get: yes
        name: python3-pip
        state: present
      # Use pip module
    - name: Install Docker python module
      pip:
        name: docker
        state: present
      # Use sysctl module
    - name: Use more memory
      sysctl:
        name: vm.max_map_count
        value: "262144"
        state: present
        reload: yes
      # Use docker_container module
    - name: download and launch a docker elk container
      docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        published_ports:
          - 5601:5601
          - 9200:9200
          - 5044:5044
      # Use systemd module
    - name: Enable service docker on boot
      systemd:
        name: docker
        enabled: yes



This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
- _ What aspect of security do load balancers protect? What is the advantage of a jump box?_
A load balancer can add additional layers of security to your website without any changes to your application. Protect applications from emerging threats The Web Application Firewall (WAF) in the load balancer protects your website from hackers and includes daily rule updates just like a virus scanner according to lumecloud.com/what-does-a-load-balancer-do .

The advantage of a jump box is is a hardened and monitored device that spans two dissimilar security zones and provides a controlled means of access between them.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _ What does Filebeat watch for?_Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. According to filbebeat overview
-  What does Metricbeat record?_Metricbeat is a lightweight shipper that records and periodically collects metrics from the operating system and from services running on the server and takes the metrics and statistics that it collects and ships them to the output that users specify, such as Elasticsearch or Logstash.|According to github.com/Moriah-team/Elk_Security

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4                  | Linux            |
| |Web-1     |       Virtual Machine   |            |   10.0.0.5               |Linux
| Web-2  |          |     Virtual Machine       |     10.0.0.6                    |Linux
| Elk        |          |            Virtual Machine|        10.2.0.4                   |Linux

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _Virtual____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _ Add whitelisted IP addresses_ 10.2.0.4

Machines within the network can only be accessed by _____.
-  Which machine did you allow to access your ELK VM? What was its IP address?_  52.165.152.169

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes             | 20.80.32.315   |
|  Web-1        |         Yes            |          20.80.30.168            |
|     Web-      Yes         |        20.80.30.168             |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-  What is the main advantage of automating configuration with Ansible?_ The main advantage of automating configuration with ansible is it saves valuable time that you can use to work on something else.

The playbook implements the following tasks:
- _ In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
To install playbook you must first start azure your jumpbox then start and attach your docker container make sure you use sudo in front 
Make sure your  in ansible. 
Next you want to nano and install your  touch /etc/ansible/install-elk.yml  nano and  edit your file .  Then ssh into your playbook and make sure it is running use the command docker ps.
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
 



Update the path with the name of your screenshot of docker ps output
file path :Project 1 Linux

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _ List the IP addresses of the machines you are monitoring  20.80.30.168 Web-1 and Web-2

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed_    filebeat and metrics beat

These Beats allow us to collect the following information from each machine:
- _ In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
File beat monitors files that you tell it to.Metricbeats statistics and also metrics 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __host___ file to container_____.
- Update the ___yml__ file to include...
- Run the playbook, and navigate to _docker ps___ to check that the installation worked as expected.

_ Answer the following questions to fill in the blanks:_
- _Which file is the playbook?install elk.yml Where do you copy it?_ into ansible
- _Which file do you update to make Ansible run the playbook on a specific machine?Host file How do I specify which machine to install the ELK server on versus which to install Filebeat on?_IP address
- _Which URL do you navigate to in order to check that the ELK server is running?
5601
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._  According to   ansible-playbook  playbook.yml
gh repo clone RJaxiii/Project-one-RJackson

