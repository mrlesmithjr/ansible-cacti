Role Name
=========

Installs and configures Cacti  
http://cacti.net/

Requirements
------------

Install requirements using Ansible Galaxy
````
sudo ansible-galaxy install -r requirements.yml -f
````

Vagrant
-------
Spin up Vagrant environment
````
vagrant up
````
Open your browser of choice and connect to:  
http://127.0.0.1:8080/cacti  
And follow the prompts to complete install.  
Log in with the following:  
````
user: admin
password: admin
````

Role Variables
--------------

````
---
# defaults file for ansible-cacti
apache2_root_dir: '/var/www/html'
cacti_config_file: '{{ cacti_site_dir }}/include/config.php'
cacti_cron_schedule:
  minute: '*/5'
  hour: '*'
  day: '*'
  month: '*'
cacti_db_info:
  host: '127.0.0.1'
  port: '3306'
  db_name: 'cactidb'
  user: 'cactiuser'
  password: 'cacti'
cacti_debian_packages:
  - php5
  - php5-cli
  - php5-gd
  - php5-mysql
  - php5-snmp
  - python-mysqldb
  - python-passlib
  - rrdtool
  - snmp
  - zlib1g
  - zlib1g-dev
cacti_dl_file: 'cacti-{{ cacti_version }}.tar.gz'
cacti_dl_url: 'http://www.cacti.net/downloads/'
cacti_site_dir: '{{ apache2_root_dir }}/cacti'
cacti_url_path: '/cacti/'
cacti_user_info:
  name: 'cactiuser'
  password: 'cacti'
  comment: 'Cacti User Account'
cacti_version: '0.8.8f'
````

Dependencies
------------

https://github.com/mrlesmithjr/ansible-apache2.git  
https://github.com/mrlesmithjr/ansible-cacti.git  
https://github.com/mrlesmithjr/ansible-mariadb-mysql.git  
https://github.com/mrlesmithjr/ansible-ntp.git  
https://github.com/mrlesmithjr/ansible-snmpd.git  
https://github.com/mrlesmithjr/ansible-timezone.git  

Install all dependencies following requirements section.

Example Playbook
----------------

#### GitHub
````
---
- hosts: all
  become: true
  vars:
    - pri_domain_name: 'vagrant.local'
  roles:
    - role: ansible-apache2
    - role: ansible-mariadb-mysql
    - role: ansible-ntp
    - role: ansible-snmpd
    - role: ansible-timezone
    - role: ansible-cacti
  tasks:
````
#### Galaxy
````
---
- hosts: all
  become: true
  vars:
    - pri_domain_name: 'vagrant.local'
  roles:
    - role: mrlesmithjr.apache2
    - role: mrlesmithjr.mariadb-mysql
    - role: mrlesmithjr.ntp
    - role: mrlesmithjr.snmpd
    - role: mrlesmithjr.timezone
    - role: mrlesmithjr.cacti
  tasks:
````

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
