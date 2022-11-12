## Ruby on Rails project deployment process

We are using AWS and this document includes two major points:
#### 1. Custom deployment over AWS.
#### 2. Domain Setup on deployed application.

Assuming we already have an AWS account to use AWS services and a purchased domain from any of domain provider.

We are going to use four major AWS services in deployment process
- AWS EC2
- AWS Volumes
- AWS Security Groups
- AWS Route53

### 1. Custom deployment for Ruby on Rails applications over AWS EC2
Here are the custom steps of complete process of deployment. 

We are choosing Ubuntu OS for our instance and documents are listed for the same.

#### Step 1. Create EC2 instance with required resources like CPU, RAM, Volume.
- Launch EC2: https://docs.aws.amazon.com/efs/latest/ug/gs-step-one-create-ec2-resources.html
- Instane types: https://aws.amazon.com/ec2/instance-types/
- Volumes: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes.html

#### Step 2: Setup security group to define required ports traffic and attach with EC2
- Basics: https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#VPCSecurityGroups
- Rules: https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#SecurityGroupRules
- Tags: https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#tagging-security-groups

#### Step 3: When EC2 launched and ready to use, check access via ssh login using given pem file
- SSH: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html
- PuTTy: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html
- WSL: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/WSL.html 

#### Step 4: Required dependencies installation like Node, Yarn, RVM, Ruby, Rails, etc.
- Node: https://www.phusionpassenger.com/library/walkthroughs/deploy/ruby/ownserver/standalone/oss/install_language_runtime.html#optional-install-node-js-if-you-re-using-rails
- Yarn: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-the-yarn-package-manager-for-node-js
- RVM: https://www.phusionpassenger.com/library/walkthroughs/deploy/ruby/ownserver/standalone/oss/install_language_runtime.html#install-rvm
- Ruby/Rails: https://www.digitalocean.com/community/tutorials/how-to-install-ruby-on-rails-with-rvm-on-ubuntu-20-04
- Mysql (When not using Cloud RDS): https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04 
- Redis: https://redis.io/docs/getting-started/installation/install-redis-on-linux/

#### Step 5: We use Nginx web server with passenger, need to install these now for clients requests handling.
- Nginx: https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04
- Passenger: https://www.phusionpassenger.com/docs/advanced_guides/install_and_upgrade/nginx/install/oss/focal.html

#### Step 6: Clone rails project repository to EC2 and follow rails setup steps including bundle, db creation, migration etc.

#### Step 7: Run seeds and other required post scripts which are needed initially.

#### Step 8: Application environment setup including:
- Configuration for git ignored secrets
- Git ignored environment variables
- Development/Staging/Production prerequisite configuration if any

#### Step 9: Creating server configurations on Nginx with below details
- Application port 
- Domain/IP
- SSL info
- Project location
- Enabled environment
- Ruby path etc.
- Setup: https://www.phusionpassenger.com/library/deploy/nginx/deploy/ruby/

#### Step 10: Restart Nginx service to load the configured changes and we are live.

### 2. Listing domain to EC2 application

#### Step 1: Purchase a domain from any domain provider

#### Step 2: Login to EC2 console and open Route53 Service
- https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring.html

#### Step 3: Create a public hosted zone for your domain
- https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/CreatingHostedZone.html

#### Step 4: Register created DNS records to your domain provider inside your DNS settings. 
- This might take couple of hours (as per domain provider) to reflect.

#### Step 5: Create a new "A" record which will point to your EC2 IP
- https://aws.amazon.com/getting-started/hands-on/get-a-domain/

#### Step 6: Reconfigure nginx server by using the domain instead of IP and point the required port.
- For SSL use port 443
- For Non-SSL use default port 80.
- Do not forget to add these ports in security group attached with EC2.
- Configuration: https://docs.nginx.com/nginx/admin-guide/web-server/web-server/


