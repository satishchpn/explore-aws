
#Use ElasticBeanStalk & RDS
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Steps To follow: 
	
	Step 1: Create Database In RDS
	Step2:  Develop Spring Boot Demp APP using the user credentials and RDS Database Config or Download the Demo Application Zip File and Update DataBase Configs
	Step7:  Create Application in Elastic BeanStalk
	Steps8: Download Postman Collection(spring-boot-aws-rds-mysql-example.postman_collection)
	Step9:  Update the Application url in Postaman APIs
	Step10: Verify the API to perform CRUD Oertaions on RDS DataBase Table Using Postman Colection

> Navigate to RDS Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Databases
	Click on Create Database
	Select Standard create
	Engine type: MYSQL
	Engine Version: MYSQL 8.0.28
	Templates: Free tier
	DB instance identifier: keshrirdsdb
	Master username: root
	Master password: password
	Come down and Under Connectivity section
	Public access: Yes
	Come down under Additional configuration section
	Initial database name: keshrirdsdb(this is schema name of our database)
	Click on create database
	Wait to see the db status as Available
	Now click on keshrirdsdb database
	Copy Endpoint & port and use it in your application db configuration
	Click on VPC security groups url under Security
	Select and Click on Security Group ID
	Under Inbound rules section Click on Edit Inbound Rules
	Click on Add Rule
	Choose Type: MYSQL/Aurora
	Source: Anywhere
	Click on Save Rule
	
> Download Spring boot Project(spring-boot-aws-rds-mysql-example.zip). 

> Unzip it and update RDS Database Configs in application.properties file and build jar file to upload into Elastic BeanStalk.
	
	> Note: Elastic Beanstalk is configured to forward requests to port 5000 by default so change the application port to 5000 if not there
		Open application.properties change server.port to 5000
		server.port=5000
		Update RDS Database Configurations
		Open cmd and type mvn clean install to create spring-boot-aws-rds-mysql-example.jar file
		
> Navigate to Elastic Beanstalk Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Create Application
	Application name: spring-boot-aws-rds-mysql-example
	Platform: Java
	Platform branch: Choose appropriate Java version(Corretto 17)
	#Optioanl Steps as db config is already provided through application.properties file
		Click on Configure more options
		Click on Database Edit
		Username: root
		Password: password
		Click on Save
		Click on Create App
		Then Once Health is OK Click on Uplaod and Deploy 
		Click on choose file
		Upload spring-boot-aws-rds-mysql-example.jar
		Click on Deploy
	Application code: Upload your code
	Source code origin: Click on choose file
	Upload spring-boot-aws-rds-mysql-example.jar
	
	Click on Create Application
	Wait to EC2 Instance get created and see Successfully launched environment: Springbootawsrdsmysqlexample-env and Health as OK(Green)
	You will find the ec2 instance application url : http://springbootawsrdsmysqlexample-env.eba-m7umiaim.us-east-1.elasticbeanstalk.com/
	
> Verify the API through Postman using CRUD Operations
		
		Update the Application url in Postaman APIs
		Call Each API to Perform CRUD Oertaions on RDS Database Table
		
		
