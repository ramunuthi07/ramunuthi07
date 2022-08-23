Ansible Installation
Ansible is an open source automation platform. It is very, very simple to setup and yet powerful. Ansible can help you with configuration management, application deployment, task automation.

Follow this in **YouTube
Prerequisites
An AWS EC2 instance
Installation steps:
Add a EPEL (Extra Packages for Enterprise Linux)third party repository to get packages for Ansible

rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
Install Ansible

yum install ansible -y 
Check Ansible version

ansible --version
Create a new user for ansible administration & grant admin access to user (Master and Slave)

useradd ansadmin
passwd ansadmin
# below command addes ansadmin to sudoers file. But strongly recommended to use "visudo" command if you are aware vi or nano editor. 
echo "ansadmin ALL=(ALL) ALL" >> /etc/sudoers
Using keybased authentication is advised. If you are still at learning stage use password based authentication (Master & Slave)

# sed command replaces "PasswordAuthentication no to yes" without editing file 
 sed -ie 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
Login as a ansadmin user on master and generate ssh key (Master)

ssh-keygen
Copy keys onto all ansible client nodes (Master)

ssh-copy-id <target-server>
Update target servers information on /etc/ansible/hosts file (Master)

echo "<target server IP>" > /etc/ansible/hosts
Run ansible command as ansadmin user it should be successful (Master)

ansible all -m ping
