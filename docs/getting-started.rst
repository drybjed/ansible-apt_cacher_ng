Getting started
===============

.. contents::
   :local:

Example inventory
-----------------

To setup Apt-Cacher NG on host given in
``debops_service_apt_cacher_ng`` Ansible inventory group:

.. code:: ini

    [debops_service_apt_cacher_ng]
    hostname

Example playbook
----------------

Here's an example playbook that can be used to install and manage Apt-Cacher NG::

    ---

    - name: Install and manage the caching HTTP proxy Apt-Cacher NG.
      hosts: [ 'debops_service_apt_cacher_ng' ]
      become: True

      roles:

        - role: debops.etc_services
          tags: [ 'role::etc_services' ]
          etc_services__dependent_list:
            - '{{ apt_cacher_ng__etc_services__dependent_list }}'

        - role: debops.apt_preferences
          tags: [ 'role::apt_preferences' ]
          apt_preferences__dependent_list:
            - '{{ apt_cacher_ng__apt_preferences__dependent_list }}'

        - role: debops.ferm
          tags: [ 'role::ferm' ]
          ferm__dependent_rules:
            - '{{ apt_cacher_ng__ferm__dependent_rules }}'


        # - role: debops.contrib-apparmor
        #   tags: [ 'role::apparmor' ]
        #   apparmor__local_dependent_config: '{{ apt_cacher_ng__apparmor__dependent_config }}'
        #   apparmor__tunables_dependent: '{{ apt_cacher_ng__apparmor__tunables_dependent }}'

        - role: debops.apt_cacher_ng
          tags: [ 'role::apt_cacher_ng' ]