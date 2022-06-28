
# Installing the Appdynamics Kubernetes cluster agent with Terraform
This repo contains shows how we can automation the installation of the AppDynamics `cluster-agent` on Kubernetes using Terraform.

## Requirements

You'll require the following to make this work in your environment:

- Kubernetes installed - we are using Intersight IKS (Intersight Kubernetes Service) Kubernetes deployed environment
- A Kubernetes `kubeconfig` file, ours is named `da-compute-kubeconfig.yml` but you can name yours with a name that makes the most sense for you but be sure to change the variable name in `terraform-appd-cluster-agent.tf`.
- Helm (we tested with version 3.3.4)
- Create your own `secret.tfvars` file with values set for variables mentioned in the lab further down in this README.md file
- Modify the variable `nsToMonitor` to ensure you are monitoring valid namespaces you would like to monitor with the Cluster Agent

## Variables values required 

Make sure the variable addressed in a terraform var files

## Credential values required in `secret.tfvar`

Terraform keeps sensitive values in a file named `secret.tfvar`and, because the values contain sensitive information such as account credentials, it's not posted here so you'll need to make one using your credentials. 

>
> Be sure to add `secret.tfvar` to your `*.gitignore` file to be sure you don't accidentally expose your credentials if you push your changes back to GitHub or other Git repository.

| Variable               | Description |
| -----------------------| ----------- |
| controller_url         | The URL of your AppDynamics Controller passed as a FQDN and port number. For example: https://example.saas.appdynamics.com:443                                                  |
| controller_account     | The account name associated with you AppDynamics Controller.            |
| controller_username    | Your username associated with the AppDynamics Controller.               |
| controller_password    | The password of your username associated with the AppDynamics Controller                                                                                         |
| controller_accessKey   | The account access key for your AppDynamics Controller.                 |

>
> Be sure to add `secret.tfvar` to your `*.gitignore` file to ensure you don't accidentally expose your credentials if you push your changes back to GitHub or other Git repository.


## Example `secret.tfvar` file
```
# AppDynamics controller credentials
controller_url       = "https://bit.saas.appdynamics.com:443"
controller_account   = "saas01"
controller_username  = "majid"
controller_password  = "mypassword"
controller_accessKey = "v11234567"
```

## Creating and Applying the Terraform Plan in command line

In this deployment, we used Terraform Business Cloud



Here are the steps needed to run Terraform along with examples of each:

1. Initialize Terraform:

`terraform init  -var-file="secret.tfvars"`

2. Create a Terraform Plan:

`terraform plan -out terraform-appd-cluster-agent-install.tfplan -var-file='secret.tfvar' `

3. Apply the Terraform Plan:

`terraform apply -var-file='secret.tfvar'`

## Results

When you successfully apply the Terraform plan, you will see information about your Kubernetes clusters reported to the AppDynamics Controller by the Kubernetes Agent. To see the information, log into your AppDynamics Controller and navigate to the Servers Tab and clicking Clusters on the left-most navigation panel.

## BayInfotech Repositories

Please visit our repositories for more detail and other projects in automation and programability:

[https://github.com/bay-infotech](https://github.com/bay-infotech)


## BayInfotech website
We are working hard to bring more automation and programmability into community. Please contact us for more detail projects and solutions

[https://bay-infotech.com](https://bay-infotech.com)

