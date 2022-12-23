
#Spring Boot Angular8 CRUD APP
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
#Use SpringBoot + AWS RDS + MYSQL + ElasticBeanStalk & S3
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Steps To follow: 
	
	Step1:  Create Database In RDS
  	Step2:  Download keshri-aws-crud-demo.zip and unzip it to get Spring Boot and Angular demo Projects.
	Step3:  Create Application in Elastic BeanStalk.
  	Step4:  Update Angular project Configs like apiendpoint url and build to generate production ready code.
	Step5:  Create S3 Bucket and deploy the Angular Application
	Step5:  Update Spring Boot APP Configs like DB Config and cors url  	
	Step6:  Deploy Spriing Boot App to Elastic Beanstalk
	Step7:  See the Hosted Website In Browser
	Step8:  Perform CRUD Operations

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
  
> Navigate to Elastic Beanstalk Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Create Application
	Application name: spring-boot-aws-rds-mysql-example
	Platform: Java
	Platform branch: Choose appropriate Java version(Corretto 17)
	Click on Create Application
	Wait to EC2 Instance get created and see Successfully launched environment: Springbootawsrdsmysqlexample-env and Health as OK(Green)
	You will find the ec2 instance application url : http://springbootawsrdsmysqlexample-env.eba-yiqszi3t.us-east-1.elasticbeanstalk.com/
  	Use this application url to update in Angular Application ApiEndpoint.
  
> Update Angular project(keshri-angular-demo). Unzip and build to later place into aws s3 bucket.

  	Open src/app/apiEndPoint.ts
  	Update baseUrl
  	baseUrl: 'http://springbootawsrdsmysqlexample-env.eba-yiqszi3t.us-east-1.elasticbeanstalk.com/api/v1/employees'
	Go to project root directory in local
	Open cmd
	Type below command to build and generate production ready code
	npm install
	ng build --configuration production
	It will create dist folder with some files inside it, it will be used to deploy to AWS
	
> Navigate to S3 Dashboard (AWS Region: US East (N. Virginia) us-east-1)

	Use the bucket if you have already or create a new bucket
	
	Click on create Bucket		
		Bucket Name: keshri-bucket
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
    		Click on Close
		
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

		It will show the Demo App Home Page    
 
> Update Spring boot Project(spring-boot-aws-rds-mysql-example). 

	Update RDS Database Configs and Angular Application url in application.properties file and build jar file to upload into Elastic BeanStalk.
	
	> Note: Elastic Beanstalk is configured to forward requests to port 5000 by default so change the application port to 5000 if not there
		Open application.properties change server.port to 5000
		server.port=5000
		Update RDS Database Configurations
		Update CORS URL
		Open cmd and type mvn clean install to create spring-boot-aws-rds-mysql-example.jar file
		
> Navigate to Elastic Beanstalk Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Springbootawsrdsmysqlexample-env
	Click on Upload and Deploy
  	Click on choose file
	Upload spring-boot-aws-rds-mysql-example.jar
	Click on Deploy
	Wait to Deploy and EC2 Instance get created and see Successfully launched environment:Springbootawsrdsmysqlexample-env and Health as OK(Green)
	You will find the ec2 instance application url : http://springbootawsrdsmysqlexample-env.eba-m7umiaim.us-east-1.elasticbeanstalk.com/
	
> Navigate to the Hosted Website In Browser

	http://keshri-bucket.s3-website-us-east-1.amazonaws.com/
	Perfom the CRUD Operations 
    
		
		
