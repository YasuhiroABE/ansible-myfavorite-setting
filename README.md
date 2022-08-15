YasuhiroABE.myfavorite-setting
==============================

This role sets up my favorite settings for ubuntu.

Requirements
------------

This role is tested on the following platforms.

### Ansible
- Version 2.9

### Distributions
- Ubuntu 20.04
- Ubuntu 22.04

Role Variables
--------------

### Defaults

    mfts_packages:
      - screen
      - mlocate
      - net-tools
      - dnsutils
      - iproute2
      - lsof
      - tcpdump
      - nmap
      - binutils
      - cron-apt
      - openssh-server
      - openntpd
    * These packages will be installed as default.

    ## setup apt repository info
    ## (e.g. "deb http://... bionic main")
    mfts_add_apt_repositories: []

    ## remove old apt repository info 
    mfts_remove_apt_repositories: []

    mfts_additional_packages: []
    * Specified packages will be installed to the system.
    
    mfts_removal_packages: []
    * Specified packages will be removed from the system.
    
    mfts_locales:
      - en_US.UTF-8
      - ja_JP.UTF-8
    * The top item will also be passed to the update-locale command.
      
    mfts_timezone: "Asia/Tokyo"
    * This value will be passed to the *timezone* module.

    mfts_sshd_listen_ipaddr: ''
    * The sshd only listens on the specified ip address.
    
    mfts_hostname: "{{ inventory_hostname }}"
    * set up hostname by the ansible hostname module.

    mfts_additional_groups: []
    * set up additional user's groups (e.g. { user: user01, groups: sudo })

    mfts_setup_directory: []
    # e.g. { path: "/etc/..", state: "directory", owner: "root", group: "root", mode: "0755" }

    mfts_copy_files: []
    * set up file information which you want to copy
    * { src:"foo.txt", dest:"/tmp/foo.txt", owner:"root", group:"root", mode:"0644" }

    mfts_sysctl_rules: []
    * set up syctl rules
    * e.g. { name: net.ipv4.ip_forward, value: 1 }

    mfts_ufw_enable: False
    # If True, UFW changes the default policy to deny.

    mfts_ufw_enable_logging: False
    # If True, UFW enables the logging mode.

    mfts_ufw_allow_rules: []
    # e.g. { type: "allow", from_ip: "10.0.0.0/8" }

    mfts_ufw_service_rules: []
    # e.g. { type: "allow", port: 22, from_ip: "10.0.0.0/8", to_ip: "192.168.1.1/32" }

    mfts_ipmasquerade_rules: []
    # If set, the iptables enables ip masquerade for the specified interface.
    # e.g. { interface: "enp1s0" }

Dependencies
------------

N/A

Example Playbook
----------------

### playbook.yaml

    - hosts: all
      vars:
        mfts_sshd_listen_ipaddr: 192.168.0.1
      roles:
        - YasuhiroABE.myfavorite-setting

### host.ini file

    [myhost]
    configured-your-hostname ansible_host=127.0.0.1

License
-------

Apache License 2.0

Author Information
------------------

[Yasuhiro ABE](http://www.yasundial.org/foaf.xml)

