# Ansible Playbook for Automation Installation & Configuration LAMP (Linux Apache MariaDB PHP) + CMS WordPress

Automate installation & configuration of CentOS Server with software package specification LAMP (Linux Apache MariaDB PHP)

## Requirements
- Git
- Ansible 2+

## Installation
First, you need to install Git and Ansible first in the master and the following commands you can follow:

```
yum install epel-release -y
yum update -y
yum install git ansible -y
```

After that, clone the required repository:
```
cd /opt/
git clone https://github.com/xnxmx/ansible-httpd-wordpress-mariadb-remotely.git
```

To see which version of Ansible is installed, type the following command:

```
ansible --version
```

The next step is to generate the SSH Key, this is done to generate the Private Key and Public Key which will be used as the authentication of the search for communication between two or more hosts, the following commands are:

```
ssh-keygen -t rsa -b 4096
```

Make changes to the host according to your needs:

```
vi /etc/ansible/hosts
```

and add the following line of code below:

```
[websrv]
192.168.1.1

[dbsrv]
192.168.1.2
```

The next process is to authenticate login on host 192.168.1.1 and 192.168.1.2, following the command:

```
ssh-copy-id root@192.168.1.1
ssh-copy-id root@192.168.1.2
```

To perform connection checks on previously added hosts, run the following commands:

```
ansible -m ping websrv
ansible -m ping dbsrv
```

To install packages and configure LAMP (Linux Apache MariaDB PHP) + CMS Wordpress, run the following command:

```
ansible-playbook /opt/ansible-httpd-wordpress-mariadb-remotely/roles/install-httpd-wordpress-mariadb-remotely.yml
```

To remove packages and configuration files LAMP (Linux Apache MariaDB PHP) + CMS WordPress, run the following command:

```
ansible-playbook /opt/ansible-httpd-wordpress-mariadb-remotely/roles/erase-httpd-wordpress-mariadb-remotely.yml
```

To install packages and configure LAMP (Linux Apache MariaDB PHP) + CMS Wordpress, also do database restoration and website content, run the following command:

```
ansible-playbook /opt/ansible-httpd-wordpress-mariadb-remotely/roles/restore-httpd-wordpress-mariadb-remotely.yml
```

## Notes
- Ansible Playbook is still tried on CentOS 7 x86_64 only
- If you are using another operating system, feel free to make changes to an existing role
- To make changes to the Ansible configuration file, you can change the following files:

```
/etc/ansible/hosts
/opt/ansible-httpd-wordpress-mariadb-remotely/.my.cnf
/opt/ansible-httpd-wordpress-mariadb-remotely/wp-config-sample.php
/opt/ansible-httpd-wordpress-mariadb-remotely/roles/erase-httpd-wordpress-mariadb-remotely.yml
/opt/ansible-httpd-wordpress-mariadb-remotely/roles/install-httpd-wordpress-mariadb-remotely.yml
/opt/ansible-httpd-wordpress-mariadb-remotely/roles/wordpress/tasks/main.yml
/opt/ansible-httpd-wordpress-mariadb-remotely/roles/httpd/defaults/main.yml
/opt/ansible-httpd-wordpress-mariadb-remotely/roles/mariadb/tasks/main.yml
/opt/ansible-httpd-wordpress-mariadb-remotely/roles/wordpress/tasks/restore.yml
/opt/ansible-httpd-wordpress-mariadb-remotely/roles/mariadb/tasks/restore.yml
```
