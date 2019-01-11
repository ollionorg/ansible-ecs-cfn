create-ecr
=========

An Ansible role to create an AWS Elastic Container repository.

Requirements
------------

This role uses cloudformation module and requires an aws configured cli.

Role Variables
-------------- 

These variables have been provided in the global scope.


| Variable | Required | Default |  Purpose |
|:---:|:---:|:---:|:---:|
| application_name   | true  |     -     | The name of the application |
| aws_region         | false | us-east-1 | The region where the resources will be created |
| assumed_role.sts_creds.access_key    | false | -  | Needs to be specified when a cross account role is being assumed.  |
| assumed_role.sts_creds.secret_key    | false | -  | Needs to be specified when a cross account role is being assumed.  |
| assumed_role.sts_creds.session_token | false | -  | Needs to be specified when a cross account role is being assumed.  


Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
        - role: create-load-balancer
          application_name: test-application
          aws_region: us-east-1

License
-------

MIT

Author Information
------------------

Sagar Gulabani
sagar.gulabani@cldcvr.com
