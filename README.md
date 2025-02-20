# Debug Assignment CDO
## Deployment Instructions

### Step 1. Clone or fork this repo
Use git to [clone](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) or [fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) this repository.

Then navigate to the directory using the terminal.

### Step 2. Prepare for Terraform

Add IAM user and add security keys to your terminal environment using the [following guide](https://docs.aws.amazon.com/cli/v1/userguide/cli-authentication-user.html).

If you have the need for a more powerful server you may want to edit the `instance_type = "t2.micro"` on line 17 in the main.tf file. Change it to your required size - see [aws docs](https://aws.amazon.com/ec2/instance-types/) for more information.

If the default AMI image fails in the future due to amazon releases you can amend line 15 in main.tf `ami = "ami-053a45fff0a704a47"` see this [guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html) to assist you. 

### Step 3. Terraform Apply
Ensure you have terraform installed by running

`terraform --version`

If not please follow the [installation instructions](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli).

Open the terraform directory with

`cd terraform`

Within this path use the following command for terraform to provision your EC2 instance. Typing `yes` when prompted to do so.

`terraform apply`

### Step 4. Ansible

#### Install Ansible

To see if ansible is installed run 

`ansible --version`

If not, please follow the [installation guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

NB: You may need to run WSL on a windows computer to run these commands, again see the guide for more information.

#### Edit config files

Open the ansible_hosts file in the ansible directory and edit the IP address, replacing it with the external [IP4 address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-ip-addresses.html#using-instance-addressing-common) of your EC2 instance.

You can check this is working with the command

`ansible -m ping all`

#### Configuring your server

To configure your server run the following commands in the given order:

`ansible-playbook playbooks/docker-install.yml`

`ansible-playbook playbooks/add-folder.yml`

You will need access to the docker-compose file on your EC2 machine. You can use the following command, replacing the items in <> with your actual values.

`scp -i <Path to your aws keys>/default-ec2.pem <Path to your repo>/docker-compose.yml ec2-user@<Public IP4 DNS Address of EC2 instance>:/home/ec2-user/devops-assessment/`

`ansible-playbook playbooks/docker-run.yml`

Default images have been built using docker and are hosted on docker hub, no additional setup is required. If you want to build your own images then changing the image names in the configuration files will be needed. If you want to host local files then you can copy these over to your EC2 instance using a similar scp command.

#### Seeing the application

In the aws console copy the Public IP4 DNS Address of EC2 instance, in a browser or postman go to `http://<your DNS address>:3000` to access your api. Or look at the following endpoints to test:

- `http://<ec2-instance-ipv4-ip-address>:3000/tour-de-france/cyclists`
- `http://<ec2-instance-ipv4-ip-address>:3000/tour-de-france/teams`
