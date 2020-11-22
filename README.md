# Ansible Role: PHP Versions

**Attention!**

This is a fork of [geerlingguy.php-versions](https://galaxy.ansible.com/geerlingguy/php-versions) role with the
[issue #46 "This role overrides php_packages, which is also used in geerlingguy.php"](https://github.com/geerlingguy/ansible-role-php-versions/issues/46)
fixed using [PR #39](https://github.com/geerlingguy/ansible-role-php-versions/pull/39). Please, feel free to use this
role if you cannot wait for corresponding PR to be merged. I will mark this role as deprecated when the original role is
fixed, but nobody knows when it will be since [Jeff Geerling](https://www.jeffgeerling.com/) is a good but
[really busy fellow](https://www.jeffgeerling.com/blog/2020/enabling-stale-issue-bot-on-my-github-repositories).

[![CI](https://github.com/webarchitect609/ansible-role-php-versions/workflows/CI/badge.svg?event=push)](https://github.com/webarchitect609/ansible-role-php-versions/actions?query=workflow%3ACI)

Allows different PHP versions to be installed when using the `geerlingguy.php` role (or a similar role). This role was originally built for [Drupal VM](https://www.drupalvm.com) but was released more generically so others could use an easier mechanism for switching PHP versions.

## Requirements

N/A

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    php_version: '7.3'

The PHP version to be installed. Any [currently-supported PHP major version](http://php.net/supported-versions.php) is a valid option (e.g. `7.2`, `7.3`, `7.4` etc.).

    php_versions_install_recommends: false

(For Debian OSes only) Whether to install recommended packages. This is set to `no` by default because setting it to `yes` often leads to multiple PHP versions being installed (thus making a bit of a mess) when using repos like Ondrej's PHP PPA for Ubuntu.

## Dependencies

  - geerlingguy.php is a soft dependency as the `php_version` variable is required to be set.
  - geerlingguy.repo-remi, if you're using CentOS or a Red Hat derivative.

## Example Playbook

    - hosts: webservers
    
      vars:
        php_version: '7.3'
    
      roles:
        - role: geerlingguy.repo-remi
          when: ansible_os_family == 'RedHat'
        - geerlingguy.php-versions
        - geerlingguy.php

## License

MIT / BSD

## Author Information

This role was created in 2017 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
