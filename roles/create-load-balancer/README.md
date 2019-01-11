create-load-balancer
=========

An Ansible role to create an AWS load balancer.

Requirements
------------

This role uses cloudformation module and requires an aws configured cli.

Role Variables
-------------- 

| Variable | Required | Default |  Purpose |
|:---:|:---:|:---:|:---:|
| application_name   | true  |     -     | The name of the application |
| env                | true  |     -     |  The name of the environment. For example staging or production |
| aws_region         | false | us-east-1 | The region where the resources will be created |
| vpc_id             | true  |     -     | The VPC Id in which the load balancer will be created. |
| alb.subnets        | true  |     -     | subnets in which load balancer nodes are created  |
| alb.security_group | false |     -     | the security group for the load balancer. If not specified one would be created.  |
| assumed_role.sts_creds.access_key    | false | -  | Needs to be specified when a cross account role is being assumed.  |
| assumed_role.sts_creds.secret_key    | false | -  | Needs to be specified when a cross account role is being assumed.  |
| assumed_role.sts_creds.session_token | false | -  | Needs to be specified when a cross account role is being assumed.  |

Dependencies
------------

aws cli

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: create-load-balancer
          application_name: test-application
          env: staging
          aws_region: us-east-1
          vpc_id: vpc_12345
          alb:
            subnets: subnet-12345,subnet-12345

          

License
-------

MIT

Author Information
------------------

Sagar Gulabani
sagar.gulabani@cldcvr.com
