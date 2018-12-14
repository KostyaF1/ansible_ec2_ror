In this Ansible project two hosts group are uses.
Hosts group 'local' uses for launch an EC2 instance. It has 'ec2' role, 'host' file into group_vars contains all needed
vars.

Host group 'webservers' uses to manage newly created EC2 instance. It has three roles: 'packages', 'ror', 'nginx'.
Role 'packages' need to update and install all needed dependencies for Ruby-on-Rails on OS.
Role 'ror' need to install Ruby and Rails.
Role 'nginx' need to install and configure Nginx web server. It has template file for configure Nginx and handler file
for restart Nginx server.
All needed vars to each role are located in 'vars' directory of each role. All groups_vars for 'webservers' group are
located in 'group_vars/webservers'.

The main playbook 'site.yml'.


Use Ansible and python-boto to launch AWS EC2 instance.
In root dir created a .boto file where 'aws_accsess_key_id' and 'aws_secret_access_key' of current AWS account are
located.
It needs to login into current AWS account.

After EC2 was launched ansible add host name of the newly created instance to the 'hosts' file into 'webservers' group.
It gets host name of EC2 instance through special 'ec2.instances' var. by using 'add_hosts' directive.

After we get a host name of newly created EC2 instance we can manage it.
In our case Ruby-on-Rails env. are installing on EC2 Ubuntu OS.
