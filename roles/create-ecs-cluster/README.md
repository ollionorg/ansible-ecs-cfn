create-ecs-cluster
=========

An Ansible role to create an AWS ECS Cluster

Requirements
------------

This role uses cloudformation. 

Role Variables
-------------- 

These variables have been provided in the global scope.

| Variable | Required | Default |  Purpose |
|:---:|:---:|:---:|:---:|
| application_name        | true  |     -     | The name of the application |
| env                     | true  |     -     |  The name of the environment. For example staging or production |
| aws_region              | false | us-east-1 | The region where the resources will be created |
| vpc_id                  | true  |     -     | The VPC Id in which the ecs cluster instances will be created. |
| ecs.instance_type       | false | t2.micro  | The instance type of ecs cluster instances.  |
| ecs.key_pair            | true  |     -     | The key pair to ssh into ecs instances          |
| ecs.security_group      | false |     -     | the security group for the ecs cluster instances. If not specified one would be created.  |     
| ecs.cluster_size        | false |     3     | The size of the ecs cluster that will be created.|
| ecs.subnets             | true  |     -     | subnets in which the ecs instances are created  |
| ecs.cluster_name        | true  |     -     | The name of the ECS cluster  |
| ecs.instance_name_tag   | true  |     -     | The name tag on the ECS instances.  |

| assumed_role.sts_creds.access_key    | false | -  | Needs to be specified when a cross account role is being assumed.  |
| assumed_role.sts_creds.secret_key    | false | -  | Needs to be specified when a cross account role is being assumed.  |
| assumed_role.sts_creds.session_token | false | -  | Needs to be specified when a cross account role is being assumed.  |

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: create-ecs-cluster
          application_name: test-application
          env: staging
          aws_region: us-east-1
          vpc_id: vpc_12345
          ecs:
            instance_type: t2.small
            key_pair: test-key-pair
            cluster_size: 2
            subnets: subnet-12345678,subnet-12345678,subnet-12345678
            cluster_name: "my-cluster-name"
            instance_name_tag: ecs-instance-name" 


License
-------

MIT

Author Information
------------------

Sagar Gulabani
sagar.gulabani@cldcvr.com
