uclalib_role_craftcms
=========

Ansible role to provision a [Craft CMS](https://www.craftcms.com) application

Requirements
------------

This role assumes the following conditions in your environment:
  * RHEL 7 OS
  * Postgres DB
  * Apache HTTPD web server
    * with mod_proxy and mod_proxy_fcgi
  * PHP 7+ installed from RHEL SCL
  * Apache proxies to PHP-FPM to serve PHP content

Role Variables
--------------

Reference `defaults/main.yml` to review default values.

Set these variables to define base project names and initial project configuration:

  * `craft_project_name` - Defines a unique project name for this instance of Craft CMS
  * `craft_app_user` - Defines the username for the initial Craft CMS project (this will be the admin user)
  * `craft_app_pass` - Defines the password for the user account for the initial Craft CMS project
  * `craft_app_email` - Defines the email address for the initial Craft CMS project
  * `craft_app_sitename` - Defines the site name for the initial Craft CMS project (e.g. `First Craft Site`)
  * `craft_app_siteurl` - Defines the URL where this instance of Craft CMS can be reached (e.g. `craft.library.ucla.edu`)

Set these variables to configure the Craft environment values:

  * `craft_environ` - Defines the craft operating environment (unless you are developing against craft, this should be set to `production`)
  * `craft_app_id` - Defines a unique identifier within craft to store session data and other information
  * `craft_security_key` - Defines a security key used to hash and encrypt data with craft
  * `craft_db_driver` - Defines the DB driver to use (can be `pgsql` or `mysql`) - this role only supports `pgsql`
  * `craft_db_server` - Defines the DB server hostname
  * `craft_db_port` - Defines the DB server connection port
  * `craft_db_name` - Defines the craft DB name
  * `craft_db_user` - Defines the craft DB username
  * `craft_db_pass` - Defines the craft DB password
  * `craft_db_schema` - Only needed for Postgres - typically this is set to `public`
  * `craft_db_table_prefix` - Defines a prefix that should be added to generated table names - this can usually be left empty

Tags
----

Use the following tags to run specific role functions:

  * `craft-setup` - download/unarchive craft
  * `craft-env` - set craft environment values
  * `craft-vhost` - set craft Apache HTTPD virtual host configuration
  * `craft-install` - perform initial craft project installation

Dependencies
------------

In general this role should work with any install of Postgres and HTTPD, however the following UCLA Library roles were used:

  * [uclalib_role_postgres](https://github.com/UCLALibrary/uclalib_role_postgresql)
  * [uclalib_role_rhelscl](https://github.com/UCLALibrary/uclalib_role_rhelscl)
  * [uclalib_role_apache](https://github.com/UCLALibrary/uclalib_role_apache)

Example Playbook
----------------

An example complete playbook would like something like the following:

```
---

- name: uclalib_craftcms.yml
  become: yes
  become_method: sudo
  hosts: all

  roles:
    - { role: uclalib_role_postgres }
    - { role: uclalib_role_rhelscl }
    - { role: uclalib_role_apache }
    - { role: uclalib_role_craftcms }
```
