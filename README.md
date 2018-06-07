Docker
=========

This role is used to set up Docker. It also has CIS embedded to configure the host for Center for Internet Security (CIS) security benchmarks for Docker v1.1.0

Requirements
------------

This role runs on Ubuntu 16.04, but has not been tested on other OSes.

Role Variables
--------------

Available variables are listed below, along with default values (see `vars/main.yml`).

```
ulimit_nofile_soft: 102400
ulimit_nofile_hard: 102400
```

We only use one set of ulimits. `nofile` can be set with a hard and soft limit. If you don't understand what these values do, leave them alone.

```
cgroup_parent: "docker"
```
This sets the cgroup that Docker will use to launch containers into. This doesn't need to change unless you really want it to.

```
userns_remap_user: "default"
```
This playbook makes use of Docker's default behaviours; if you set the `userns-remap` to `default`, Docker will create a user called `dockeremap`. If you wish to change this, please [check the Docker guide for setting up a namespace user.](https://docs.docker.com/engine/security/userns-remap/#enable-userns-remap-on-the-daemon).

```
tls_verify: true
tls_ca_cert: /path/to/ca/cert
tls_cert: /path/to/cert
tls_key: /path/to/key
```
If you want to set up TLS for Docker, change the above values to point to where you have placed your TLS certificates and keys.

Dependencies
------------
None.

Example Playbook
----------------

Playbooks can utilize the CIS role without much effort:

    - hosts: all
      roles:
        - ansible-docker

The role is thoroughly tagged so that you can run certain sections or certain levels of checks:

    # Test only items from section 4
    ansible-playbook -i hosts -C playbook.yml -t section1

    # Apply changes only from items in section 4, 5, and 6
    ansible-playbook -i hosts playbook.yml -t section4,section5,section6

License
-------

Apache License, Version 2.0
