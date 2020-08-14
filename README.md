freehck.redis_standalone
=========

Deploy a redis standalone instance in docker container

Description
-----------

This role is for simple one-node redis deployment when you need to quickly setup some test environment. You can also use it in production environment (f.e. if it's used by php application, as zen php driver has numerous issues when works with cluster redis).

Role Variables
--------------

**Container variables**

`redis_standalone_ct_name`: `"redis"`

`redis_standalone_ct_image`: `"bitnami/redis:5.0.9"`

`redis_standalone_ct_restart_policy`: `"always"`

`redis_standalone_ct_state`: `"started"`

`redis_standalone_ct_restart`: `"{{ ct_restart | default(false) }}"`

`redis_standalone_ct_pull`: `"{{ ct_pull | default(true) }}"`

`redis_standalone_ct_recreate`: `"{{ ct_recreate | default(false) }}"`


**Network variables**

`redis_standalone_bind_ip`: not set by default, because it's dangerous to allow redis to listen an external interface interface

`redis_standalone_port`: `"6379"`


**Files and directories**

`redis_standalone_env_file_template`: `"env.j2"`

`redis_standalone_srv_dir`: `"/srv/{{ redis_standalone_ct_name }}"`

`redis_standalone_env_file`: `"{{ redis_standalone_srv_dir }}/env"`

`redis_standalone_data_dir`: `"{{ redis_standalone_srv_dir }}/data"`


**Service configuration**

`redis_standalone_allow_empty_password`: `"yes"`

`redis_standalone_redis_password`: `""`


Example
-------

    - hosts:
        - redis
      become: true
      roles:
        - role: freehck.pkg_install
          pkg_install_packages:
            - docker.io
            - python3-pip
        - role: freehck.pip_install
          pip_install_packages:
            - docker
        - role: freehck.redis_standalone
          redis_standalone_bind_ip: "{{ ansible_host }}"


Install
-------

This role can be installed from [Ansible Galaxy](https://galaxy.ansible.com/):

`ansible-galaxy install freehck.redis_standalone`

License
-------

MIT

Author Information
------------------

Dmitrii Kashin, <freehck@freehck.ru>
