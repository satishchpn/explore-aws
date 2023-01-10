#Use Spring Boot , Docker , AWS ECS , AWS ECR , AWS FarGate
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Download Spring boot Project(keshri-spring-boot-aws-crud-demo.zip). Unzip it and build docker image.

	Create Docker Imgae
	
		Start Docker Daemon
		Open CMD at Project root directory and type below command
		mvn spring-boot:build-image
		after successful image creation run below command to see if image is created
		To list the images
		docker image ls
		docker run --tty --publish 8080:5000 keshri-spring-boot-aws-crud-demo:0.0.1-SNAPSHOT
		open browser and see if api is working
		<docker_host>:8080
		
	
> Login to AWS account

	UN: cloud_user
	Password: <password>
	
> Note: Always make sure that you have selected AWS Region: US East (N. Virginia) us-east-1

> Navigate to IAM Dashboard (AWS Region: US East (N. Virginia) us-east-1)

	Create a User Group
	Click on User Groups
	Click on create Group
	User group name: keshri_user_group
	Select Policies: IAMFullAccess , AdministratorAccess
	Click on Create Group

	Create a User
		Click on Users
		Click on Add Users
		User name: keshri_admin_user
		Select AWS access type: Access key - Programmatic access , AWS Management Console access
		Console password: Pass@123
		Require password reset: UnSelect
		Click on Next Permissions
		Select keshri_user_group
		Click on Next Tags
		Click on Next Review
		Click on Create User
		After Successful creation of User you will get Access Key Id and Secret Access Key, 
		Copy and keep with you, it will be used tpo connect to DynamoDB from Application
		Access key ID: AKIA5MFQEV3DFJPNYP32
		Secret access key : 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
		If Not found then Click on that User and In Access Keys Section
		Click on Create Access Key to get the access key and secret key
		Click on Close

> Navigate to ECR Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Create Repository
	
		Click on Create Repository Get Started
		Repository name: keshri-registry
		Click on Create Registry
		Select keshri-registry
		Click on View Push commands (Use this command later to push the image to ECR)

> Install AWS CLI

	Go to this link and follow the steps given or folloow the steps below
	
		https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
	
	Open cmd in admin mode and type below command to install AWS CLI
	
		> msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
	
	To Confirm Installation type below command in cmd to see AWS CLI version
	
		> aws --version

> Configure AWS

	Open cmd and type below commands
	
		> aws configure
			AWS Access Key ID [None]: AKIA5MFQEV3DFJPNYP32
			AWS Secret Access Key [None]: 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
			Default region name [None]: us-east-1
			Default output format [None]: json
 	
		> aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 919492406982.dkr.ecr.us-east-1.amazonaws.com
		
			It will give output as Login Succeeded
			
		> docker tag keshri-spring-boot-aws-crud-demo:0.0.1-SNAPSHOT 919492406982.dkr.ecr.us-east-1.amazonaws.com/keshri-registry
		
		> docker push 919492406982.dkr.ecr.us-east-1.amazonaws.com/keshri-registry

> Navigate to ECR Dashboard (AWS Region: US East (N. Virginia) us-east-1)

	Select keshri-registry
	Refresh and see the pushed image
	Copy the Image URI which will be used later to deploy to ECS
	Image URI: 919492406982.dkr.ecr.us-east-1.amazonaws.com/keshri-registry:latest
		
> Navigate to ECS Dashboard (AWS Region: US East (N. Virginia) us-east-1)

	Create Task Defination

		Click on Task Defination
		Click on create new Task Defination
		Launch type: FARGATE
		Click on Next Step
		Task definition name: keshri-spring-boot-ecs-example
		Task role: None
		Task memory (GB): 1 GB
		Task CPU (vCPU): 0.5vCPU
		Click on Add Container
		Container name: keshri-docker-container
		Image: docker.io/satishchpn/keshri-spring-boot-aws-crud-demo:0.0.1-SNAPSHOT
		Memory Limits (MiB): Hard Limit (1024)
		Port mappings: 
		Container port: 8080
		Click on Add port mapping
		Container port: 80
		Click on Add
		Click on Create
		Click on View Task Definition

	Create Cluster

		Click on Clusters
		Click on Create Cluster
		Select Networking only
		Click on Next Step
		Cluster name: keshri-aws-cluster
		Tags
			Key: aws-cluster
			Value: keshri-aws-cluster
		Click on Create
		Click on View Cluster
		Click on Tasks Tab
		Click on Run new Task
		Launch type: FARGATE
		Task Definition: keshri-spring-boot-ecs-example
		Cluster: keshri-aws-cluster
		Select Cluster VPC : choose default one
		Subnets: choose first one
		Security groups: Click on edit
		Assigned security groups: Create new security group
		Security group name: keshri-security-group
		Inbound rules for security group
		Type: ALL TCP
		Click on Add rule
		Type: ALL Traffic
		Click on Save
		Click on Run Task
		Now select keshri-spring-boot-ecs-example task definition and open in new browser
		In Chcek if the Status is RUNNING
		Expand or Select the container and in Detail Network Section Find IP
		From Network Section find Public IP: 3.235.98.186
		

> See the API Result In Browser

		http://3.235.98.186:5000/
		Hi Keshri - Welcome to AWS
		
		http://3.235.98.186:5000/employees
		See List of Employees
	
