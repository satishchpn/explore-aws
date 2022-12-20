# explore-aws

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Use IAM , S3 , EC2
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------




#Deploy Spring Boot application to AWS
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Download Spring boot Project(spring-boot-aws-example.zip). Unzip it and build jar to later place into aws s3 bucket.
	Open cmd and type mvn clean install to create spring-boot-aws-example.jar


> Login to AWS account
	UN: cloud_user
	Password: <password>
	
> Note: Always make sure that you have selected AWS Region: US East (N. Virginia) us-east-1

> Navigate to IAM Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Roles
	
		Click on create Role
		Trusted entity type:AWS Service
		Use case:EC2
		Click on Next
		Click on create Policy
		Choose  Service:S3 & Access Analyzer using add addition policy
		Actions:all access
		Resources:All resources
		Click on next tags
		Click on Next review
		Name:keshri_policy
		Click On create policy
		Refresh Roles page
		Choose AmazonS3FullAccess,keshri_policy
		Click on Next
		Role Name:keshri_role
		Click on create Role

> Navigate to S3 Dashboard (AWS Region: US East (N. Virginia) us-east-1)

		Click on create Bucket
		
		Bucket Name:keshri-bucket
		AWS Region: US East (N. Virginia) us-east-1
		De-Select : Block all public access
		Select : I acknowledge
		Click on create Bucket

		Click on keshri-bucket
		Go to permissions tab 
		Click on Edit Bucket Policy
		Paste below policy JSON
			{
				   "Version":"2012-10-17",
				   "Id":"Policy1671206715413",
				   "Statement":[
					  {
						 "Sid":"Stmt1671206713512",
						 "Effect":"Allow",
						 "Principal":"*",
						 "Action":"s3:*",
						 "Resource":"arn:aws:s3:::keshri-bucket/*"
					  }
				   ]
			}
			
		Click on Save changes
		
		Click on Buckets
		Select keshri-bucket (will able to see access as public)
		Click on Upload
		Drop spring-boot-aws-example.jar
		Click on Upload
		Now click on uploaded jar to see the details
		Object URL it will be used later to download the jar from keshri_ec2: https://keshri-bucket.s3.amazonaws.com/spring-boot-aws-example.jar

> Navigate to EC2 Dashboard(AWS Region: US East (N. Virginia) us-east-1)
	
		Click on Launch Instance
		
		Name:keshri_ec2
		Click on Create new key pair
		Key pair name:keshri_ec2
		Key pair type:RSA
		Private key file format:.ppk
		Click on create key pair
		Save the download file keshri_ec2.ppk locally so later that can be used to connect through putty

		Click on Edit Network settings
		Under Inbound security groups rules click on add security group rule
		Type:Custom TCP
		Port Range:5000 (Intentionally given as later In elastic beanstalk default port is 5000 so keeping common across all example)
		SourceType:Anywhere
		Click Advanced Details
		Choose IAM Instance Profile:keshri_role
		Click on Launch Instance

> Connect to keshri_ec2 EC2 instance using Putty

		Go to EC2
		
		Click on Instances
		Select keshri_ec2 to see the details
		Copy Public IPv4 DNS: ec2-54-157-252-131.compute-1.amazonaws.com
		
		Open Putty
		
		Host name : ec2-54-157-252-131.compute-1.amazonaws.com
		Click on Connection>
		Click On Data
		UserName=ec2-user
		Click on Ssh
		Click on Auth
		Click on Credentials
		Choose Private key file:browse and locate the keshri_ec2.ppk
		Click on Session
		Give name in Saved Session: keshri_aws_instance
		Click on Open
		Click on accept
		
		After successful login	type below commands in Putty Terminal
		
		Putty Terminal
		
		sudo -i
		yum install java
		y
		alternatives --config java(command to check java versions availbale on that ec2 instance)
		aws s3 ls(To see available s3 bucket access- keshri-bucket)
		Download the jar from s3 bucket to keshri_ec2 instance
		wget <jar_url>
		wget https://keshri-bucket.s3.amazonaws.com/spring-boot-aws-example.jar
		ls
		Run the Jar
		java -jar spring-boot-aws-example.jar

> See the API Result In Browser

		http://ec2-54-157-252-131.compute-1.amazonaws.com:5000
		Hi Keshri - Welcome to AWS
		
		http://ec2-54-157-252-131.compute-1.amazonaws.com:5000/home
		Welcome Keshri to First Spring Boot - AWS Deployment Demo

	

#Deploy Angular application to AWS
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Download Angular project(keshri-angular-demo.zip). Unzip and build to later place into aws s3 bucket.

	Go to project root directory in local
	Open cmd
	Type below command to build and generate production ready code
	npm install
	ng build --configuration production
	It will create dist folder with some files inside it, it will be used to deploy to AWS
	
> Navigate to S3 Dashboard (AWS Region: US East (N. Virginia) us-east-1)

	Use the bucket if you have already or create a new bucket
	
	Click on create Bucket		
		Bucket Name:keshri-bucket
		AWS Region: US East (N. Virginia) us-east-1
		De-Select : Block all public access
		Select : I acknowledge
		Click on create Bucket
		
		Click on keshri-bucket
		Go to permissions tab 
		Click on Edit Bucket Policy
		Paste below policy JSON
			{
				   "Version":"2012-10-17",
				   "Id":"Policy1671206715413",
				   "Statement":[
					  {
						 "Sid":"Stmt1671206713512",
						 "Effect":"Allow",
						 "Principal":"*",
						 "Action":"s3:*",
						 "Resource":"arn:aws:s3:::keshri-bucket/*"
					  }
				   ]
			}
			
		Click on Save changes
		
		Click on Buckets
		Select keshri-bucket (will able to see access as public)
		
		Now Upload all the files from application dist/keshri-angular-demo folder to AWS Bucket
		
		Click on keshri-bucket
		Click on Upload
		Drag and drop all the files from application dist/keshri-angular-demo to keshri-bucket
		Click on Upload
		
		Now Go to keshri-bucket properties tab
		Click on Edit Static website hosting
		Static website hosting:Enable
		Index document:index.html
		Click on Save Changes
		
		Again go to keshri-bucket properties tab
		Go to Static website hosting section
		Use Bucket website endpoint to open in the browser
			

> See the Hosted Website In Browser

		http://keshri-bucket.s3-website-us-east-1.amazonaws.com/

		It will show List of Universities In India
			
			
			
# Use ElasticBeanStalk
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Login to AWS account
	UN: cloud_user
	Password: <password>
			
> Note: Always make sure that you have selected AWS Region: US East (N. Virginia) us-east-1
	
> Steps To follow: 
	
	Step 1: Create Table
	Step 2: Create a User Group
	Step3 : Create a User
	Step4 : Create a Policy
	Step5 : Attach the Policy To User Group
	Step6: Develop the Spring Boot Demp APP using the user credentials and DynamoDB Details or Download the demo Application Zip File
	Step7: Create Application in Elastic BeanStalk
	
> Download Spring boot Project(spring-boot-aws-example.zip). Unzip it and build jar file to later upload into Elastic BeanStalk.
	
	> Note: Elastic Beanstalk is configured to forward requests to port 5000 by default so change the application port to 5000 if not there
		Open application.properties change server.port to 5000
		server.port=5000
		Open cmd and type mvn clean install to create spring-boot-aws-example.jar file

> Navigate to DynamoDB Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	Click on Create Table
	Table Name: Employee
	Primary Key: employeeId(String)
	Click on Create Table
	Table got Created , now to access this table from Java Application we have to create User Group,User and Policy e.t.c

> Navigate to IAM Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Create a User Group
		Click on User Groups
		Click on create Group
		User group name: keshri_user_group
		Select Policies: AmazonEC2FullAccess , AdministratorAccess
		Click on Create Group
	
	Create a User
		Click on Users
		User name: keshri_admin_user
		Select AWS access type: Access key - Programmatic access
		Click on Next Permissions
		Select keshri_user_group
		Click on Next Tags
		Click on Next Review
		Click on Create User
		After Successful creation of User you will get Access Key Id and Secret Access Key, 
		Copy and keep with you, it will be used tpo connect to DynamoDB from Application
		Access key ID: AKIARSFB3NQWJBSFXZAD
		Secret access key : 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
		Click on Close
	
	Create Policy
		Click on Policies
		Click on Create Policy
		Choose  Service: DynamoDB & Access Analyzer using add addition policy
		Actions:all access
		Resources:All resources
		Click on next tags
		Click on Next review
		Name:keshri_dynamo_db_policy
		Click On Create policy
	
	Attch this Policy to User Group
		Search policy : keshri_dynamo_db_policy
		Select that policy
		Click on Action
		Click On Attach Policy
		Select keshri_user_group
		Click on Attach Policy
			

> Navigate to Elastic Beanstalk Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Create Application
	Application name: spring-boot-aws-dynamodb-example
	Platform: Java
	Platform branch: Choose appropriate Java version(Corretto 17)
	Application code: Upload your code
	Source code origin: Click on choose file
	Upload spring-boot-aws-dynamodb-example.jar
	Click on Create Application
	Wait to EC2 Instance get created and see Successfully launched environment: Springbootawsexample-env and Health as OK(Green)
	You will find the ec2 instance application url : http://springbootawsexample-env.eba-fuepzbxp.us-east-1.elasticbeanstalk.com/
	
> See the API Result In Browser

		http://springbootawsexample-env.eba-fuepzbxp.us-east-1.elasticbeanstalk.com/
		Hi Keshri - Welcome to AWS
			
		http://springbootawsexample-env.eba-fuepzbxp.us-east-1.elasticbeanstalk.com/home
		Welcome Keshri to First Spring Boot - AWS Deployment Demo	

			
			
# Use ElasticBeanStalk & DynamoDB
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------


> Download Spring boot Project(spring-boot-aws-dynamodb-example.zip). Unzip it and build jar file to later upload into Elastic BeanStalk.
	
	> Note: Elastic Beanstalk is configured to forward requests to port 5000 by default so change the application port to 5000 if not there
		Open application.properties change server.port to 5000
		server.port=5000
		Open cmd and type mvn clean install to create spring-boot-aws-dynamodb-example.jar file
			

> Login to AWS account
	UN: cloud_user
	Password: <password>


	
	
	
	
	
	
#Open Source API
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

	https://github.com/Hipo/university-domains-list
	http://universities.hipolabs.com/search?country=india
	https://mixedanalytics.com/blog/list-actually-free-open-no-auth-needed-apis/
	https://datausa.io/api/data?drilldowns=Nation&measures=Population

