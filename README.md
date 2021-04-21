Role Name
=========

Use this role to configure the kubernetes worker node launched on AWS 

Requirements
------------

1. Provisioned instances on AWS 
```
ansible-galaxy install inshiyanalawala.k8s_cluster_on_aws
```
2. Configured the master node of kubernetes using an ansible role as follows: 
```
ansible-galaxy install inshiyanalawala.k8s_master_config_ansible_role
```

2. Edit the k8s_cluster_on_aws/vars/main.yml file 
   Provide valid credentials and configuration of the instances here to be used by the role to provision cluster 

  ```
  - hosts: localhost
    roles:
     - role: "k8s_cluster_on_aws"
```

Now, after provisiong the cluster on AWS, configure dynamic ec2 inventory to be able to configure the instances on AWS.

``` wget https://raw.githubusercontent.com/vshn/ansible-dynamic-inventory-ec2/master/ec2.py
    wget https://raw.githubusercontent.com/vshn/ansible-dynamic-inventory-ec2/master/ec2.ini
```
Next, export a few variables 

```export AWS_ACCESS_KEY_ID=’<your access key>'
   export AWS_SECRET_ACCESS_KEY=’<your secret key>'
   export EC2_INI_PATH=/path/to/my_ec2.ini
   export ANSIBLE_HOSTS=/path/to/ec2.py
```    
    
Configure ssh-agent forwarding to log into instances with your key. 
1. Copy the .pem key file used to configure instances in the ~/.ssh directory on your system
2. Run the following commands

``` ssh-agent bash
    ssh-add ~/.ssh/<your-key>.pem
```
Finally, make the script files excutable

``` 
chmod +x e2.py
    
chmod +x ec2.ini
```    
    
Example Playbook
----------------

    - hosts: tag_kubernetes_master
      roles:
         - role: "k8s_master_config_ansible_role"

    - hosts: tag_kubernetes_worker
      roles:
        - roles: "k8s_master_config_ansible_role"
