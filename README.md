Role Name: My Favorite Settings
=========

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
	* These packages will be installed as default.
 	
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
	
Dependencies
------------

N/A

Example Playbook
----------------

    - hosts: all
      roles:
	    - ansible-myfavorite-setting

License
-------

Apache License 2.0

Author Information
------------------

[Yasuhiro ABE](http://www.yasundial.org/foaf.xml)

