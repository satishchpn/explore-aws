

#Use ElasticBeanStalk , RDS & ASM(AWS Secret Manager)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Steps To follow: 
	
	Step1: Create Database In RDS
  	Step2: Store Secret to ASM(AWS Secret Manager)
	Step3: Develop Spring Boot Demp APP using the user credentials and RDS Database Config or Download the Demo Application Zip File and Update the Configs
	Step4: Create Application in Elastic BeanStalk
	Step5: Download Postman Collection(spring-boot-aws-rds-mysql-example.postman_collection)
	Step6:  Update the Application url in Postaman APIs
	Step7: Verify the API to perform CRUD Oertaions on RDS DataBase Table Using Postman Colection

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

> Navigate to Secrets Manager Dashboard (AWS Region: US East (N. Virginia) us-east-1)

	  Click on Store a new Secret
	  Secret type: Credentials for Amazon RDS database
	  Credentials
	    User name: root
	    Password: password
	  Select Database
	  DB Instance: keshrirdsdb
	  Click on Next
	  Secret name: keshri-db-credentails
	  Click on Next
	  Here you can enable/disable automatic Secret rotation based on need
	  Click on Next
	  Under Sample Code Section copy Java Code which we will use later in our application
	  Click on Store
   
> Download Spring boot Project(spring-boot-aws-rds-mysql-asm-example.zip). 

> Unzip it and update RDS Database Configs in application.properties file and build jar file to upload into Elastic BeanStalk.
	
> Note: Elastic Beanstalk is configured to forward requests to port 5000 by default so change the application port to 5000 if not there
		Open application.properties change server.port to 5000
		server.port=5000
		Update RDS Database Configurations like secret manager name, schemaName , region , accessKey and secretKey
		
    To Get Access Key and Secret key
      Navigate to AWS Management Console
      On Top Right Corenr click on Logged in user
      Click on Security Credentails
      Under Access keys Click on Create access Key
      Select Application running on an AWS compute service
      Click the Acknowledge checkbox
      Click on Next
      Description tag value: keshri-admin-user
      Copy the credentils      
      Access key: AKIAYHH3AUCECTZPIWUX
      Secret access key: WurrzfPKFAjbQrzAGC0RgCCG+tM8GJA7U9z4AySA
      Click on Done
		Open cmd and type mvn clean install to create spring-boot-aws-rds-mysql-asm-example.jar file
		
> Navigate to Elastic Beanstalk Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Create Application
	Application name: spring-boot-aws-rds-mysql-asm-example
	Platform: Java
	Platform branch: Choose appropriate Java version(Corretto 17)
	Application code: Upload your code
	Source code origin: Click on choose file
	Upload spring-boot-aws-rds-mysql-asm-example.jar
	
	Click on Create Application
	Wait to EC2 Instance get created and see Successfully launched environment: Springbootawsrdsmysqlasmexample-env and Health as OK(Green)
	You will find the ec2 instance application url : http://springbootawsrdsmysqlexample-env.eba-m7umiaim.us-east-1.elasticbeanstalk.com/
	
> Verify the API through Postman using CRUD Operations
		
		Update the Application url in Postaman APIs
		Call Each API to Perform CRUD Oertaions on RDS Database Table
		
		
