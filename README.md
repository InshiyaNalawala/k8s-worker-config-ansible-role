Role Name
=========

Use this role to configure the kubernetes worker node launched on AWS 

Requirements
------------

1. Provisioned instances on AWS (use the 'cluster' role - https://github.com/InshiyaNalawala/kubernetes-cluster/tree/master/roles/cluster )
2. Tag the worker instance as - "kubernetes":"worker"
3. Configure the master using this role - https://github.com/InshiyaNalawala/kubernetes-cluster/tree/master/roles/k8s_worker


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: tag_kubernetes_worker
      roles:
         - role: k8s_worker
