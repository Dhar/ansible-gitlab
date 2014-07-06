Gitlab
======

Installs [GitLab](https://github.com/gitlabhq/gitlabhq/) from git.
Generally follows the installation document on their site, but uses MySQL instead of Postgresql. Uses Nginx as a frontend.

Requirements
------------

This role was created on/for Ubuntu Trusty installations and was specifically tested in an OpenVZ container environment.

Role Variables
--------------

The role uses the following variables, set in the defaults/main.yml file:

* `gitlab_branch` - The specific GitLab branch to clone
* `gitlab_shell_version` - The specific GitLab Shell branch to clone
* `gitlab_db_host` - Hostname of the GitLab database server
* `gitlab_db_name` - Name of the GitLab database to create
* `gitlab_db_user` - Username of the database user
* `gitlab_db_passwd` - Password of the database user
* `gitlab_user` - Username of the GitLab system user to create
* `gitlab_ssh_port` - GitLab Shell SSH port number 
* `gitlab_hostname` - Hostname of the GitLab web server
* `gitlab_use_gmail` - Flag to enable sending email via Gmail instead of using local sendmail
* `gitlab_email_from` - Email address to send email from
* `gitlab_email_password` - Password of above email account

Dependencies
------------

Depends on the [joshualund.ruby-2_0_0](https://galaxy.ansible.com/list#/roles/145), [DavidWittman.redis](https://galaxy.ansible.com/list#/roles/730), and [Ansibles.mysql](https://galaxy.ansible.com/list#/roles/509) roles.  See playbook examples for integration of GitLab variables with other roles.

Usage
-----

    ansible-galaxy install garnold.gitlab

Also check the [Ansible Galaxy](https://galaxy.ansibleworks.com/intro) about page.

Example Playbook
-------------------------

Example playbook for installing GitLab database and web servers on separate systems:

    ---
    - hosts: gitlab-db
      roles:
      - { role: Ansibles.mysql, mysql_databases: [{name: "{{ gitlab_db_name }}"}], mysql_users: [{name: "{{ gitlab_db_user }}", pass: "{{ gitlab_db_passwd }}", host: "{{ gitlab_hostname }}", priv: "{{ gitlab_db_name }}.*:ALL"}]}
    
    - hosts: gitlab
      roles:
      - { role: ansible-gitlab, gitlab_db_host: "{{ gitlab_db_host }}" }

License
-------

MIT

Author Information
------------------

Gary Arnold

[GitHub project page](https://github.com/Dhar/ansible-gitlab)
