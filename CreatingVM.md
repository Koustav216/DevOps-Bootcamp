- We can create and use an AWS instance using AWS console i.e. using the UI.

- But as a DevOps engineer we may get numerous requests daily to create VMs for different purposes.

- In such cases, it is efficient to write a script for creating AWS instances i.e. using Automation. AWS provides AWS EC2 API to create and manage EC2 instances. We can write scripts to communicate with this AWS EC2 API. 

- The request send to the AWS API would be validated,authenticated and authorized by AWS.

- There are multiple ways to create a script to talk to the API, e.g. using
  - AWS CLI
  - AWS API
  - AWS CFT (Cloud Formation Template)
  - AWS CDK (Cloud Development Kit)

- VM is also termed as an **infrastructure**.

- In case of Hybrid Cloud Model (i.e. different cloud providers are used for fulfilling different purposes of an organization) Terraform is useful. 

## Steps to create EC2 instance using UI

If we have to create only one instance, we may use this approach:

- First, login to AWS Management Console.

- Under services, go to **Compute** . Choose  **EC2** .

- Click on **Launch Instance**.

- Provide a name, select required OS.

- Always check whether the provided Instance type is eligible for Free tier.

- Under Key pair, click on Create new key pair.

- Provide a name . Keep the Key pair type and Private key file format default (i.e. RSA and .pem respectively) . Click on Create key pair.
  - The downloaded .pem file should be stored in a secured location always.

- Under Network Settings make sure ,

  - Auto-assign public IP is enabled.
  - Type is set to ssh.
  - Source type is set to Anywhere.

- Click on launch instance.

- Now, we can either connect using the UI i.e.
  - Select the EC2 instance
  - Click on Connect button. Again click on Connect button when the Connect to instance windown appears.

- Or, we can use any terminal (e.g. MOBAXTERM) to connect to our instance.

- When we are done, make sure to Stop instance and Terminate instance under Instance state (after selecting a particular instance).

## Steps to connect an existing EC2 instance to MOBAXTERM (using UI)

- Open MOBAXTERM and click on Session.

- Click on SSH.

- Get the public IPv4 address of the instance and paste it in the Remote host.

- Check Specify username box and provide a username. 

- Click on Advanced SSH settings and check Use private key box. Upload the .pem file associated with the instance.

- Click on OK to connect to the instance. (Click on 'Accept' if any pop-up window appears).

## Steps to SSH into the EC2 instance from a terminal

Here, we would take a look at the steps to SSH into our EC2 instance using `ssh` command. We would require the the key-value file (private key) associated with the instance.

Make sure the permisson bits of the key-value file looks like this `-rwx------` i.e. none other than the user should have access to this file, otherwise we shall get error while connecting.

- Open a  terminal. 

- Type `ssh -i <path_to_key-value_file> <default_username_of_ec2>@<public_IPAddress_of_ec2>`

  - For example, `ssh -i ./helloworldPasskey.pem ubuntu@16.170.242.189`
  - Here, **-i** stands for **identity file**.
  - As we have created a Ubuntu machine, the deafult username is **ubuntu**.
  
    ![this](./assets/default_username_aws.JPG)

- Type yes to connect.

- We can disconnect using `logout` command. To reconnect, we need to use the **ssh** command again.

## Steps to connect AWS CLI with AWS account

The AWS Command Line Interface (AWS CLI) is a unified tool that provides a consistent interface for interacting with all parts of Amazon Web Services. To follow the steps mentioned below, make sure that AWS CLI is installed.

After installing the CLI, we need to connect it to our AWS account. For that, we need to get/create the ACCESS KEY ID and SECRET ACCESS KEY from Security Credentials on AWS Console. The latter can only be accessed while creating a new access key.

- Type `aws configure` in a terminal.

- Enter the **ACCESS KEY ID**

- Enter the **SECRET ACCESS KEY**

- Enter the default region name as **us-east-1**

- Enter the default output format as **json**

Now we can execute any command to interact with the AWS API.

We can refer any command for CLI from [here](https://docs.aws.amazon.com/cli/latest/reference)

## Create Resources using AWS Cloud Formation Templates

- Using CFT we can talk to AWS api and create resources. 

- We can refer to the sample templates from [here](https://github.com/awslabs/aws-cloudformation-templates)

- Search by **CFT** in the search bar and choose CloudFormation.

- Click on **Create stack** and there we can upload our template or create one from scratch.

## Connecting to the AWS API using a scripting language

- We can use Shell script or Python or any scripting language.

- Python supports a package **boto3** . Using it we can automate our requirements very easily. If we have **AWS CLI** installed, it will get the configuration details from there.
