
#Use Spring Boot , GitHub , Docker, CodeBuild , CodePipeline , ECR , ECS , FarGate
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Create Spring boot Project(keshri-spring-boot-aws-crud-demo) in GitHub(https://github.com/satishchpn/keshri-spring-boot-aws-crud-demo)

> Login to AWS account

	UN: cloud_user
	Password: <password>
	
> Note: Always make sure that you have selected AWS Region: US East (N. Virginia) us-east-1

> Navigate to ECR Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Create Repository
	
		Click on Create a Repository Get Started
		Repository name: keshri-registry
		Click on Create Repository
		Select keshri-registry
		Click on View Push commands (Use this command later to push the image to ECR)

> Navigate to CodeBuild Dashboard (AWS Region: US East (N. Virginia) us-east-1) to create and push Docker Image to ECR
	
	Click on Create build project
	Project name: keshri-demo-project-code-build
	Select Source provider: GitHub
	Click on Connect to GitHub
	Grant the Access
	Repository URL: <https://github.com/xyz>
	Operating system: Amazon Linux 2
	Runtime(s): Standard
	Image: choose latest one(4.0)
	Privileged: tick or enable this flag
	Role: sleect existing or create new role (codebuild-keshri-demo-project-service-role)
	Click on create build project

> Navigate to IAM Dashboard (AWS Region: US East (N. Virginia) us-east-1)

	Click on Roles
	Search codebuild-keshri-demo-project-service-role
	Select that role
	Click on Add permissions
	Click on Attach Policies
	Select these policies : AmazonEC2ContainerRegistryFullAccess,AmazonEC2ContainerRegistryPowerUser
	Click on Attach Policies

> Navigate to CodeBuild Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Start Build

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
	
