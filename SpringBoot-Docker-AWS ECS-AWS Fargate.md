#Use Spring Boot , Docker , AWS ECS , AWS FarGate
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
		Login to docker account
		docker login -u satishchpn
		Add tag to docker image using docker username(satishchpn)
		docker tag keshri-spring-boot-aws-crud-demo:0.0.1-SNAPSHOT satishchpn/keshri-spring-boot-aws-crud-demo:0.0.1-SNAPSHOT
	
	Push Docker Image to DockerHub
	
		docker push satishchpn/keshri-spring-boot-aws-crud-demo:0.0.1-SNAPSHOT
		see if this image available in logged-in dockerhub dashboard


> Login to AWS account

	UN: cloud_user
	Password: <password>
	
> Note: Always make sure that you have selected AWS Region: US East (N. Virginia) us-east-1

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
		Click on Create
		Click on View Cluster
		Click on Tasks
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
		Expand the container and in Detail Section click on View logs in CloudWatch
		From Network Section find Public IP: 3.215.182.136
		

> See the API Result In Browser

		http://3.215.182.136:5000/
		Hi Keshri - Welcome to AWS
		
		http://3.215.182.136:5000/employees
		See List of Employees
	
