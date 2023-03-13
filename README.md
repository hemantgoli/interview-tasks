# interview-tasks
# govtech-test



## Getting started

# Task 1

1. Created private S3 bucket using terraform code and copied the incremental-decremental html page to the created bucket ( "govtech-webpages")

2. Created Terraform configuration script to deploys an Auto Scaling group, EC2 instances running Nginx web server behind an Application Load Balancer (ALB) on AWS. 

	Following Components are used to create the end to end deployment

		aws_security_group	: to incoming traffic on port 80 (HTTP).
		aws_eip			: Elastic IP address for the instances.
		aws_subnet			: creates two subnets in different availability zones to ensure high availability and fault tolerance.
		aws_vpc			: VPC with a /16 CIDR block, DNS support, and DNS hostnames enabled.
		aws_internet_gateway	: Internet Gateway to allow traffic to and from the internet.
		aws_route_table		: public route table and associates it with the VPC and the Internet Gateway.
		aws_launch_configuration: launch configuration for the instances
		aws_alb			: Application Load Balancer with two subnets and a security group.
		aws_lb_listener		: listener for the ALB on port 80 and forwards traffic to the target group.
		aws_alb_target_group	: target group for the instances and performs health checks on the root path.
		aws_autoscaling_group	: Auto Scaling group with three instances

3. Created Gitlab deploy to update the code 

	It defines two stages, "deploy" and "refresh"

	deploy stage : to synchronize the contents of the current directory with an S3 bucket named "govtech-webpages" then copies a specific file from the S3 bucket to itself and replace the content. This stage is only executed when changes are pushed to the "master" branch.

	refresh stage:  also uses the Amazon AWS CLI tool to adjust the desired capacity of an Auto Scaling group named "govtech-autoscl-grp" to 0, and then to 3, effectively refreshing the instances in the group. This stage is also only executed when changes are pushed to the "master" branch.



#Task 2
1. Created a Docker image for the Incremental and Decremental Count page in nginx image

2. Push the Docker images to a docker registry : docker push  hemantgoli/govtech-test:01

3. Created a Kubernetes deployment for the nginx and MySQL server using the Docker image

