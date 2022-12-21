#Use ElasticBeanStalk & DynamoDB
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Steps To follow: 
	
	Step 1: Create Table In DynamoDB
	Step 2: Create a User Group in IAM
	Step3 : Create a User in IAM
	Step4 : Create a Policy in IAM
	Step5 : Attach the Policy To User Group
	Step6:  Develop the Spring Boot Demp APP using the user credentials and DynamoDB Config or Download the Demo Application Zip File and Update DynamoDB Configs
	Step7:  Create Application in Elastic BeanStalk
	Steps8: Download Postman Collection(springboot-dynamodb-api-collection)
	Step9:  Update the Application url in Postaman APIs
	Step10: Verify the API to perform CRUD Oertaions on DynamoDB Table Using Postman Colection

> Navigate to DynamoDB Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Create Table
	Table Name: Employee
	Partition key: employeeId(String)
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
		Click on Add Users
		User name: keshri_admin_user
		Select AWS access type: Access key - Programmatic access
		Click on Next Permissions
		Select keshri_user_group
		Click on Next Tags
		Click on Next Review
		Click on Create User
		After Successful creation of User you will get Access Key Id and Secret Access Key, 
		Copy and keep with you, it will be used tpo connect to DynamoDB from Application
		Access key ID: AKIAZPWCPFWX5OPZ6AFB
		Secret access key : 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
		Click on Close
	
	Create Policy
		Click on Policies
		Click on Create Policy
		Choose  Service: DynamoDB & SNS using add addition policy
		Actions:all access
		Resources:All resources
		Click on next tags
		Click on Next review
		Name: keshri_dynamo_db_policy
		Click On Create policy
	
	Attch this Policy to User Group
		Search policy : keshri_dynamo_db_policy
		Select that policy
		Click on Actions
		Click On Attach
		Select keshri_user_group
		Click on Attach Policy
			
> Download Spring boot Project(spring-boot-aws-dynamodb-example.zip). 

> Unzip it and update DynamoDB Configs in application.properties file and build jar file to upload into Elastic BeanStalk.
	
	> Note: Elastic Beanstalk is configured to forward requests to port 5000 by default so change the application port to 5000 if not there
		Open application.properties change server.port to 5000
		server.port=5000
		Update DynamoDB Configurations
		Open cmd and type mvn clean install to create spring-boot-aws-dynamodb-example.jar file
		
> Navigate to Elastic Beanstalk Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Create Application
	Application name: spring-boot-aws-dynamodb-example
	Platform: Java
	Platform branch: Choose appropriate Java version(Corretto 17)
	Application code: Upload your code
	Source code origin: Click on choose file
	Upload spring-boot-aws-dynamodb-example.jar
	Click on Create Application
	Wait to EC2 Instance get created and see Successfully launched environment: Springbootawsdynamodbexample-env and Health as OK(Green)
	You will find the ec2 instance application url : http://springbootawsdynamodbexample-env.eba-pdkhfjup.us-east-1.elasticbeanstalk.com/
	
> Verify the API through Postman using CRUD Operations
		
		Update the Application url in Postaman APIs
		Call Each API to Perform CRUD Oertaions on DynamoDB Table
		
		
