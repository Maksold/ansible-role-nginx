Ansible NGINX Role
==================

[![Ansible Galaxy](https://img.shields.io/badge/galaxy-nginxinc.nginx-5bbdbf.svg)](https://galaxy.ansible.com/nginxinc/nginx)
[![Build Status](https://travis-ci.org/nginxinc/ansible-role-nginx.svg?branch=master)](https://travis-ci.org/nginxinc/ansible-role-nginx)

This role installs NGINX Open Source, NGINX Plus, the NGINX Amplify agent, or NGINX Unit on your target host.

**Note:** This role is still in active development. There may be unidentified issues and the role variables may change as development continues.

Changes made by [Maksold](https://github.com/maksold) for Magento 2.x compatibility
------------

**Default variables**

The following files are new or has changes:

-   **defaults/main/template.yml:** Remove unnecessary variables, enable nginx_main_template, nginx_http_template by default.
-   **defaults/main/magento2.yml:** Add variables for Magento 2 specific templates.
-   **defaults/main/logrotate.yml:** Enable logrotate by default and changed logrotate options.

**Templates**

The following files are new or has changes:

-   **templates/nginx.conf.j2:** Totally replace main nginx config file 
-   **templates/fastcgi_params:** Add fastcgi params
-   **templates/conf.d/default.conf:** Default server block to ignore non-existing server names
-   **templates/conf.d/magento2.conf:** Magento 2 server config
-   **templates/conf.d/magento2/assets.conf:** Manage /static and /media URIs
-   **templates/conf.d/magento2/extra_protect.conf:** Deny access to specific files and limit_req (zone1, zone2, zone3) for specific URIs
-   **templates/conf.d/magento2/maintenance.conf:** Allow to enable maintenance mode
-   **templates/conf.d/magento2/maps.conf:** Maping for PHP-FPM pass route, HTTP auth, multi shop code configuration, good/bad user agents
-   **templates/conf.d/magento2/php_backend.conf:** Add headers for php and configure fastcgi params
-   **templates/conf.d/magento2/rabbitmq_proxy.conf:** RabbitMQ proxy (like /rabbitmq/*)
-   **templates/conf.d/magento2/status.conf:** Server status for localhost (like /nginx_status, /status, /ping)
-   **templates/conf.d/magento2/varnish_proxy.conf:** Varnish proxy config (pass, headers, timeout) **Temporary disabled!**

**Tasks**

The following files has changes:

-   **tasks/conf/logrotate.yml:** Ignore errors for Logrotate run

Requirements
------------

**Ansible**

This role was developed and tested with [maintained](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#release-status) versions of Ansible. Backwards compatibility is not guaranteed.

Instructions on how to install Ansible can be found in the [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

**Molecule**

Molecule is used to test the various functionailities of the role. Instructions on how to install Molecule can be found in the [Molecule website](https://molecule.readthedocs.io/en/latest/installation.html).

Installation
------------

**Ansible Galaxy**

Use `ansible-galaxy install nginxinc.nginx` to install the latest stable release of the role on your system.

**Git**

Use `git clone https://github.com/nginxinc/ansible-role-nginx.git` to pull the latest edge commit of the role from GitHub.

Platforms
---------

The NGINX Ansible role supports all platforms supported by [NGINX Open Source](https://nginx.org/en/linux_packages.html#mainline), [NGINX Plus](https://www.nginx.com/products/technical-specs/), the [NGINX Amplify agent](https://github.com/nginxinc/nginx-amplify-doc/blob/master/amplify-faq.md#21-what-operating-systems-are-supported), and [NGINX Unit](https://unit.nginx.org/installation/#official-packages):

**NGINX Open Source**

```yaml
Alpine:
  versions:
    - 3.8
    - 3.9
    - 3.10
    - 3.11
CentOS:
  versions:
    - 6
    - 7
    - 8
Debian:
  versions:
    - stretch
    - buster
FreeBSD:
  versions:
    - 11.2+
    - 12
RedHat:
  versions:
    - 6
    - 7.4+
    - 8
SUSE/SLES:
  versions:
    - 12
    - 15
Ubuntu:
  versions:
    - xenial
    - bionic
    - focal
```

**NGINX Plus**

```yaml
Alpine:
  versions:
    - 3.8
    - 3.9
    - 3.10
    - 3.11
Amazon Linux:
  versions:
    - 2018.03
Amazon Linux 2:
  versions:
    - any
CentOS:
  versions:
    - 6.5+
    - 7.4+
    - 8
Debian:
  versions:
    - stretch
    - buster
FreeBSD:
  versions:
    - 11.2+
    - 12
Oracle Linux:
  versions:
    - 6.5+
    - 7.4+
RedHat:
  versions:
    - 6.5+
    - 7.4+
    - 8
SUSE/SLES:
  versions:
    - 12
    - 15
Ubuntu:
  versions:
    - xenial
    - bionic
    - focal
```

**NGINX Amplify Agent**

```yaml
Amazon Linux:
  versions:
    - 2017.09
CentOS:
  versions:
    - 6
    - 7
Debian:
  versions:
    - jessie
    - stretch
RedHat:
  versions:
    - 6
    - 7
Ubuntu:
  versions:
    - xenial
    - bionic
    - focal
```

**NGINX Unit**

```yaml
Amazon Linux:
  versions:
    - 2018.03
Amazon Linux 2:
  versions:
    - any
CentOS:
  versions:
    - 6
    - 7
    - 8
Debian:
  versions:
    - stretch
    - buster
RedHat:
  versions:
    - 6
    - 7
    - 8
Ubuntu:
  versions:
    - xenial
    - bionic
    - focal
```

Role Variables
--------------

This role has multiple variables. The descriptions and defaults for all these variables can be found in the **`defaults/main`** directory in the following files:

-   **[defaults/main/main.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/defaults/main/main.yml):** NGINX installation variables
-   **[defaults/main/amplify.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/defaults/main/amplify.yml):** NGINX Amplify agent installation variables
-   **[defaults/main/template.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/defaults/main/template.yml):** NGINX configuration templating variables
-   **[defaults/main/upload.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/defaults/main/upload.yml):** NGINX configuration/HTML/SSL upload variables
-   **[defaults/main/linux.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/defaults/main/linux.yml):** Linux installation variables
-   **[defaults/main/bsd.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/defaults/main/bsd.yml):** BSD installation variables
-   **[defaults/main/unit.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/defaults/main/unit.yml):** NGINX Unit installation variables

Example Playbooks
-----------------

Working functional playbook examples can be found in the **`molecule/common`** directory in the following files:

-   **[molecule/common/playbooks/default_converge.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/molecule/common/playbooks/default_converge.yml):** Install a specific version of NGINX and set up logrotate
-   **[molecule/common/playbooks/module_converge.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/molecule/common/playbooks/module_converge.yml):** Install various NGINX supported modules
-   **[molecule/common/playbooks/source_converge.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/molecule/common/playbooks/source_converge.yml):** Install NGINX from source
-   **[molecule/common/playbooks/stable_push_converge.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/molecule/common/playbooks/stable_push_converge.yml):** Install NGINX using the stable branch and push a preexisting config from your system to your NGINX instance
-   **[molecule/common/playbooks/template_converge.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/molecule/common/playbooks/template_converge.yml):** Use the NGINX configuration templating variables to create an NGINX configuration file
-   **[molecule/common/playbooks/unit_converge.yml](https://github.com/nginxinc/ansible-role-nginx/blob/master/molecule/common/playbooks/unit_converge.yml):** Install NGINX Unit

Do note that if you install this repository via Ansible Galaxy, you will have to replace the role variable in the sample playbooks from `ansible-role-nginx` to `nginxinc.nginx`.

Other NGINX Roles
-----------------

You can find an Ansible collection of roles to help you install and configure NGINX Controller [here](https://github.com/nginxinc/ansible-collection-nginx_controller)

You can find an Ansible role to help you install and configure NGINX App Protect [here](https://github.com/nginxinc/ansible-role-nginx-app-protect)

License
-------

[Apache License, Version 2.0](https://github.com/nginxinc/ansible-role-nginx/blob/master/LICENSE)

Author Information
------------------

[Alessandro Fael Garcia](https://github.com/alessfg)

[Grzegorz Dzien](https://github.com/gdzien)

[Tom Gamull](https://github.com/magicalyak)

&copy; [NGINX, Inc.](https://www.nginx.com/) 2018 - 2020
