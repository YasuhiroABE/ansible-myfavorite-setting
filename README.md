YasuhiroABE.myfavorite-setting
==============================

This role sets up my favorite settings.

Requirements
------------

This role is tested on the following platforms.

### Ansible
- Version 2.4

### Distributions
- Ubuntu 16.04
- Debian 9

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
    
    mfts_hostname: "{{ ansible_hostname }}"
    * set up hostname by the ansible hostname module.

    mfts_additional_groups: []
    * set up additional user's groups (e.g. { user: user01, groups: sudo })

    mfts_copy_files: []
    * set up file information which you want to copy
    * { src:"foo.txt", dest:"/tmp/foo.txt", owner:"root", group:"root", mode:"0644" }

    mfts_sysctl_rules: []
    * set up syctl rules
    * e.g. { name: net.ipv4.ip_forward, value: 1 }

Dependencies
------------

N/A

Example Playbook
----------------

    - hosts: all
      vars:
        mfts_sshd_listen_hostprefix: 192.168.0.1
      roles:
        - YasuhiroABE.myfavorite-setting

License
-------

Apache License 2.0

Author Information
------------------

[Yasuhiro ABE](http://www.yasundial.org/foaf.xml)

