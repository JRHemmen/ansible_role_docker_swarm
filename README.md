docker_swarm
=========

A role to install docker and initialize a swarm. All hosts with this role assigned will have docker installed and be joined to the swarm. Manager nodes are defined when host var swarm_master=true

Requirements
------------

A group in Ansible's inventory titled docker. The first host in this group MUST be a manager and have swarm_master=true defined.

Example inventory file
-----------------------

    [docker]
    docker-01 ip_address=192.168.1.94 swarm_master=true
    docker-02 ip_address=192.168.1.95 swarm_master=true
    docker-03 ip_address=192.168.1.96 swarm_master=true
    docker-04 ip_address=192.168.1.97
    docker-05 ip_address=192.168.1.98
    docker-06 ip_address=192.168.1.99



Role Variables
--------------

    overlay_networks: a list of overlay networks (provided as strings) to create on the swarm. Default is 1 network named dockernet.

Dependencies
------------

None.

Example Playbook
----------------

    - name: Configure swarm
      hosts: docker
      become: yes
      vars:
        - overlay_networks:
          - network1
          - network2
          
      roles:
        - jrhemmen.docker_swarm_node
      tags:
        - swarm_node

         ---


License
-------

GPLv3
