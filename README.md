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

    mfts_lineinfile_after_copyfiles: []  ## default: state: "present"
    # execute lineinfile module after copying files
    # e.g. - { path: "/etc/ca-certificates.conf", regexp: "^local/www.example.com.crt$", line: "local/www.example.com.crt", state: "present" }

    mfts_command_after_copyfiles: [] ## default: become: "no"
    # execute command after executing ilninfile module
    # e.g. - { command: "echo Hello", become: "no" }  ## Note: the default value of become is "no"

    mfts_sysctl_rules: []
    * set up syctl rules
    * e.g. { name: net.ipv4.ip_forward, value: 1 }

    mfts_ufw_enable: false
    # If True, UFW changes the default policy to deny.

    mfts_ufw_enable_logging: false
    # If True, UFW enables the logging mode.

    mfts_ufw_allow_rules: []
    # e.g. { type: "allow", from_ip: "10.0.0.0/8" }

    mfts_ufw_service_rules: []
    # e.g. { type: "allow", port: 22, from_ip: "10.0.0.0/8", to_ip: "192.168.1.1/32" }

    mfts_ipmasquerade_rules: []
    # If set, the iptables enables ip masquerade for the specified interface.
    # e.g. { interface: "enp1s0" }

    mfts_systemd_rules: [] ## default: enabled: "no", daemon_reload: "no"
    # e.g. { name: "nginx.service", state: "started", enabled: "yes", daemon_reload: "no" }

Dependencies
------------

N/A

Example Playbook
----------------

### An example of a playbook.yaml file

    - hosts: all
      vars:
        mfts_sshd_listen_ipaddr: 192.168.0.1
      roles:
        - YasuhiroABE.myfavorite-setting

### An example playbook of ufw firewall rules for nginx

    - hosts: all
      vars:
        mfts_ufw_enable: True
        mfts_ufw_enable_logging: True
        mfts_ufw_service_rules:
          - { type: "allow", port: "80", from_ip: "0.0.0.0/0", to_ip: "192.168.1.1/32" }
          - { type: "allow", port: "443", from_ip: "0.0.0.0/0", to_ip: "192.168.1.1/32" }

### An example playbook of copying TSL certificate and key files

    - hosts: all
      vars:
        mfts_additional_packages:
          - ca-certificates
          - nginx
        mfts_setup_directory:
          - { path: "/usr/share/ca-certificates/local", state: "directory", owner: "root", group: "root", mode: "0755" }
        mfts_copy_files:
          - { src: "{{ inventory_dir }}/files/nginx/server.conf", dest: "/etc/nginx/conf.d/server.conf", owner: "root", group: "root", mode: "0644" }
          - { src: "{{ inventory_dir }}/files/nginx/www.example.com.crt", dest: "/usr/share/ca-certificates/local/www.example.com.crt", owner: "root", group: "root", mode: "0644" }
          - { src: "{{ inventory_dir }}/files/nginx/www.example.com.nopass.key", dest: "/etc/ssl/private/www.example.com.nopass.key", owner: "root", group: "root", mode: "0640" }
        mfts_lineinfile_after_copyfiles:
          - { path: "/etc/ca-certificates.conf", regexp: "^local/www.example.com.crt$", line: "local/www.example.com.crt" }
        mfts_command_after_copyfiles:
          - { command: "/usr/sbin/update-ca-certificates", become: "yes" }
        mfts_systemd_rules:
          - { name: "nginx.service", state: "started", enabled: "yes", daemon_reload: "no" }
      roles:
        - YasuhiroABE.myfavorite-setting

License
-------

Apache License 2.0

Author Information
------------------

[Yasuhiro ABE](http://www.yasundial.org/foaf.xml)

