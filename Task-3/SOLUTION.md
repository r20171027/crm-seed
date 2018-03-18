# Install and configure Ansible AWX

Make folder test3 in project folder and copy to test3 playbooks, created in Task-2 .
For install Ansible AWX use VM createrd from Vagrantfile.(add) 

in Vagrantfile:
##   First update the OS:
     sudo yum -y update

##   Install requisite base packages:
      sudo yum -y install bzip2 device-mapper-persistent-data gcc gcc-c++ git gettext lvm2 yum-utils

##    Add the EPEL and Docker repositories:
      sudo yum -y install epel-release
      sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
      sudo yum -y update

##    Install Ansible and pip:
      sudo yum -y install ansible python-pip

##    Set up Docker CE:
       sudo yum -y install docker-ce
       sudo systemctl enable docker
       sudo systemctl start docker

##    Install docker-py via pip:
      sudo pip install -U docker-py	

## start VM with command 
'vagrant up --provision'

--------------------------------------------------------------------------------------
On console VM:

Change /etc/ansible/ansible.cfg:
remote_user = root
log_path = /project/.ansible/ansible.log


Change /etc/ansible/hosts:
[test]
10.0.2.15

As root, clone and deploy AWX to Docker containers via Ansible:
-  git clone   https://github.com/ansible/awx.git
-  cd awx/installer/
- start install:
   ansible-playbook -i inventory install.yml
 - Monitor migrations status :
   docker logs -f awx_task


- for use local playbooks copy folder test3 into /var/lib/awx/projects


Start browser with url http://127.0.0.1:8000

INVENTORIES  > CREATE INVENTORY > my_inventory

INVENTORIES  my_inventory   HOSTS >   test

PROJECTS  > CREATE PROJECT > test_git (use playbooks on Git)

Set the SCM Type Git
Set the SCM URL Type https://github.com/r20171027/crm-seed.git

PROJECTS  > CREATE PROJECT> test_local (use local playbook)

Set the SCM Type Manual 
and select test3



TEMPLATES >  CREATE JOB TEMPLATE > install docker

use project test_git  for use playbooks from Git or project test_local  for use local playbooks
 


***************************************************

inst-docker.yml -  Ansible install docker and tools

crm-present.yml - Ansible  presentation project

present-stop.yml - Ansible  stop presentation project

crm-compile.yml - Ansible  compile project

crm-tests.yml - Ansible  sbt running test

crm-running.yml - Ansible  crm running 





