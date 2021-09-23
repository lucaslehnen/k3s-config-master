Configure a k3s node to be a master node
=========

This role can be used together with:

  - https://github.com/lucaslehnen/k3s-install -> prepare
  - https://github.com/lucaslehnen/k3s-config-worker -> Worker node
  - https://github.com/lucaslehnen/k3s-reset -> Reset

Configure the variables
-----------------------

`master_ip` :  

The k3s master node IP;

`extra_server_args` : 

Extra args that can be passed to the service. 
Check the k3s documentation: https://rancher.com/docs/k3s/latest/en/installation/install-options/server-config/

`ansible_user` : 

User to configure access to Kubernetes cluster via CLI/kubectl

Example
----------------

In your `main.yml`:

```yaml
- hosts: servers
  roles:
      - k3s-config-master
  vars:
    master_ip: "192.168.99.11"
    ansible_user: ubuntu
    extra_server_args: "--write-kubeconfig-mode 644"
```

In your `requirements.yml`:

```yaml
- name: k3s-config-master
  src: https://github.com/lucaslehnen/k3s-config-master
  version: v1.0.0
```

Define target hosts in your inventory file `hosts`:

    [servers]
    192.168.99.11
    192.168.99.12
    192.168.99.13

Install requirements:

```
ansible-galaxy install -r requirements.yml
```

Call the playbook:

    ansible-playbook -i hosts main.yml

License
-------

MIT

Author
------------------

https://github.com/lucaslehnen
