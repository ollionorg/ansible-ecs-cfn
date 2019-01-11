
# AWS ECS Infrastructure Deployer

<p align = "center">
<img src="assets/logoStack.png" alt="cloudcover" width="300"/>
</p>

[Prerequisites](#prerequisites)  
[How To Run](#How%20To%20Run)  
[Variables](#Variables)
[License](#License)
[Contributions](#Contributions)



An Ansible playbook used to create and deploy cloudformation stacks for ECS infrastructure resources on AWS. 
ECS is one of the most popular services used to deploy containers on AWS today. 
However the infrastructure for an ECS cluster has a number of resources that need to be managed. Managing these resources manually would be a pain. Using this Ansible playbook managing ECS resources would become very easy.

It creates the following resources

1. An ECS Cluster
2. A Load balancer along with listeners and target groups.
3. An Elastic container repository
4. Security Groups where not specified.

## Prerequisites

1. You should use an AWS Configured CLI to run this Ansible playbook (AWS CLI is pre-installed and profile is configured on your machine).
2. If you wish to create the resources in another account, make sure you have the cross account role ready.
3. Have an AWS Key pair ready (PEM file).
4. Have atleast two subnets in two different availablity zones ready.
5. Have two security groups ready, one for your ECS cluster instances and one for your loadbalancer. If you do not specify security groups , they will be automatically created. 
6.  In case you use your own security groups, make sure to allow traffic from the load balancer security group to your ECS Instance security group.

## How To Run

1. Create a copy of the file `configs/config.yml` and name it as `project.environmentname.config.yml`. 
2. Replace project and environmentname in the filename according to your environment name and project name, for e.g. `myapp.staging.config.yml`
3. Edit the file and set the variables appropriately as described [below](#variables).
4. Run the command from the shell `ansible-playbook create-resources-ansible.yml --extra-vars "config_file =myapp.staging.config.yml"`
5. In case you do not want to specify the environment variable, edit the `config.yml` file already present in the repository with your configuration. The ansible automatically picks up this file.

## Variables

Please look into the sample file for a clear example.

#### About the Application 

This section gives information about the application which helps in naming the stacks.

- **`application_name`** : The name of the application.
- **`aws_region`** : The region where the resources have to be created.
- **`env`** : The environment name for the resources that are being created.
- **`role_arn`** : The role arn for the account if the resources are being created with cross account. Comment this line if you want to create the resources in the account to which the creds belong and there is no need to assume any cross account role.
- **`vpc_id`** : The vpc id where the infrastructure will be setup.

#### About the ECS Cluster

- **`ecs.instance_type`** : The instance type to use for the cluster, for e.g. `t2.medium`
- **`ecs.key_pair`** : The keypair name to be passed for cluster instances that are being created.
- **`ecs.security_group`** : The security group of the ECS instance. Should allow traffic from the load balancer on ports 30000 to 60000. Optional. It is optional. If you do not specify this field, a security group will be created for you.
- **`ecs.cluster_size`** : The cluster size of the ECS Cluster.
- **`ecs.subnets`** : A comma separated list of the subnets to be used for creating instances of the cluster.
- **`ecs.cluster_name`** : The cluster name.
- **`ecs.instance_name_tag`** : The name to be given to the instances of the cluster.

#### About the Load Balancer

- **`alb.subnets`** : The subnets containing a load balancer node. Should be public subnets and should belong to atleast two different availability zones
- **`alb.security_group`** : The security group of the load balancer. This load balancer allows traffic from the public on port 80 and port 443. It is optional. If you do not specify this field, a security group will be created for you.

## License

MIT

## Contributions

Everybody is welcome to contribute. Please, see [`contributing`][contrib] for further information.

[contrib]: CONTRIBUTING.md

