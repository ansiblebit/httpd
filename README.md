# httpd

[![License](https://img.shields.io/badge/license-New%20BSD-blue.svg?style=flat)](https://raw.githubusercontent.com/ansiblebit/httpd/master/LICENSE)
[![Build Status](https://travis-ci.org/ansiblebit/httpd.svg?branch=master)](https://travis-ci.org/ansiblebit/httpd)

[![Platform](http://img.shields.io/badge/platform-ubuntu-dd4814.svg?style=flat)](#)

[![Project Stats](https://www.openhub.net/p/ansiblebit-httpd/widgets/project_thin_badge.gif)](https://www.openhub.net/p/ansiblebit-httpd/)

[Ansible][ansible] role to setup the [Apache HTTP server][apache].

Currently only the `package` installation is tested and working properly.

The `source` installation currently has a problem when building the code.


## Tests

| Family | Distribution | Version | Test Status |
|:-:|:-:|:-:|:-:|
| Debian | Debian  | Jessie  | [![x86_64](http://img.shields.io/badge/x86_64-passed-006400.svg?style=flat)](#) |
| Debian | Debian  | Wheezy  | [![x86_64](http://img.shields.io/badge/x86_64-passed-006400.svg?style=flat)](#) |
| Debian | Ubuntu  | Yakkety | [![x86_64](http://img.shields.io/badge/x86_64-passed-006400.svg?style=flat)](#) |
| Debian | Ubuntu  | Xenial  | [![x86_64](http://img.shields.io/badge/x86_64-passed-006400.svg?style=flat)](#) |
| Debian | Ubuntu  | Wily    | [![x86_64](http://img.shields.io/badge/x86_64-passed-006400.svg?style=flat)](#) |
| Debian | Ubuntu  | Trusty  | [![x86_64](http://img.shields.io/badge/x86_64-passed-006400.svg?style=flat)](#) |
| Debian | Ubuntu  | Precise | [![x86_64](http://img.shields.io/badge/x86_64-passed-006400.svg?style=flat)](#) |


## Requirements

- ansible >= 2.0


## Role Variables

- **debug**: flag to run debug tasks.
- **httpd_conf**: configuration settings for `{{ httpd_dir_configuration }}/conf-{available|enabled}`.
- **httpd_configuration**: contents of the `{{ httpd_dir_configuration }}/httpd.conf` file.
- **httpd_default**: contents of `/etc/default/{{ httpd_service }}`.
- **httpd_dir_cache**: directory for [apache][apache] cache.
- **httpd_dir_configuration**: directory for [apache][apache] configuration.
- **httpd_dir_install**: directory where [apache][apache] will be installed.
- **httpd_dir_lib**: directory where [apache][apache] modules are located.
- **httpd_dir_lock**: directory where [apache][apache]....
- **httpd_dir_run**: directory where [apache][apache] PID file will be stored.
- **httpd_installation**: the installation method: `build` or `package`.
- **httpd_modules**: list of [apache][apache] modules.
- **httpd_modules_dynamic**: list of dynamically linked [apache][apache] modules.
- **httpd_modules_static**: list of statically linked [apache][apache] modules.
- **httpd_ports**: list of ports [apache][apache] will be listening to.
- **httpd_service**: name of the service: `apache2` for package installations; `httpd` otherwise.
- **httpd_sites**: list of available sites.
- **httpd_user**: user under which apache will be running.
- **httpd_version**: the [apache][apache] version to be installed.


### package

Variables specific to the `package` installation process.

- **httpd_configuration_envvars**: configuration for the `/etc/apache2/envvars` file.


### build

Variables specific to the `build` installation process.

- **httpd_build_dependencies**: list of packages needed to build [apache][apache].
- **httpd_build_options**: option to be passed to `configure`.
- **httpd_dir**: symlink to the enabled [apache][apache] installation.
- **httpd_dir_source**: directory where to build [apache][apache].
- **httpd_env**: environment variables.
- **httpd_environment**: [apache][apache] environment.
- **httpd_force_build**: flag to indicate if a build is to be triggered no matter the server state.
- **httpd_download_url**: the URL for the tarball.
- **httpd_download_url_asc**: the URL for the tarball PGP signature.
- **httpd_download_url_md5**: the URL for the tarball MD5 checksum.
- **httpd_mpm_module**: the mpm [apache][apache] module.
- **httpd_pid_file**: path to the [apache][apache] PID file.
- **httpd_tarball**: filename of the tarball.


## Dependencies

None.


## Playbooks

    - hosts: servers
      vars:
        see tests/vars/vagrant.yml
    
      roles:
         - role: ansiblebit.httpd


## Tags

- **configuration**: configuration tasks.
- **debug**: task to debug role variables.
- **installation**: installation tasks.
- **validation**: task to validate role variables.


## Test

To run the tests you will need to install:

- [tox](https://tox.readthedocs.org/)
- [vagrant](https://www.vagrantup.com/)

To run all tests against all pre-defined OS/distributions * ansible versions:

```
$ tox
```

To run tests for `trusty64`:

```
$ cd tests
$ bash test_idempotence.sh --box trusty64.vagrant.dev
# log file will be stores under tests/log
```

To perform debugging on a specific environment:

```
$ cd tests
$ vagrant up trusty64.vagrant.dev

# to provision using the test.yml playbook (as many time as you need)
$ vagrant provision trusty64.vagrant.dev

# to access the Vagrant box
$ vagrant ssh trusty64.vagrant.dev
```


## Links

- [Apache > HTTP Server > Documentation](http://httpd.apache.org/docs/)
- [Apache > HTTP Server > Documentation > Version 2.4 > Compiling and Installing](https://httpd.apache.org/docs/current/install.html)
- [Apache > HTTP Server > Documentation > Version 2.4 > Programs > configure - Configure the source tree](https://httpd.apache.org/docs/current/programs/configure.html)
- [Verifying Apache HTTP Server Releases](http://httpd.apache.org/dev/verification.html)


[ansible]:  https://ansible.com/    "Ansible"
[apache]:   http://httpd.apache.org/    "Apache HTTP server"
