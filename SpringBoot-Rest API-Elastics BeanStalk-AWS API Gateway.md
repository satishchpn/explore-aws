#Use Spring Boot Rest ,  ElasticBeanStalk , AWS API Gateway
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
  
Download Spring boot Project(spring-boot-rest-aws-api-gateway-example). Unzip it and build jar file to later upload into Elastic BeanStalk.
  
> Note: Elastic Beanstalk is configured to forward requests to port 5000 by default so change the application port to 5000 if not there

    Open application.properties change server.port to 5000
    server.port=5000
    Open cmd and type mvn clean install to create spring-boot-rest-aws-api-gateway-example file
    
> Login to AWS account
    UN: cloud_user
    Password: <password>
			
> Note: Always make sure that you have selected AWS Region: US East (N. Virginia) us-east-1

> Navigate to Elastic Beanstalk Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
    Click on Create Application
    Application name: spring-boot-rest-aws-api-gateway-example
    Platform: Java
    Platform branch: Choose appropriate Java version(Corretto 17)
    Application code: Upload your code
    Source code origin: Click on choose file
    Upload spring-boot-rest-aws-api-gateway-example.jar
    Click on Create Application
    Wait to EC2 Instance get created and see Successfully launched environment: Springbootrestawsapigatewayexample-env and Health as OK(Green)
    You will find the ec2 instance application url : http://springbootrestawsapigatewayexample-env.eba-u2izsrft.us-east-1.elasticbeanstalk.com/

> Navigate to API Gateway Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on Build REST API
	Choose the protocol: Rest
	Create new API: New
	API Name: keshri-employee-service
	Click on Create API
	Click on Actions
	Click on Create Resource
	Resource Name: keshri-employee-service
	Click on Create Resource
	Click on Actions
	Click on Create Method
	Select GET Type
	Click on tick to create it.
	Integration type: HTTP
	Select Use HTTP Proxy integration
	Endpoint URL: http://springbootrestawsapigatewayexample-env.eba-u2izsrft.us-east-1.elasticbeanstalk.com/employees
	Click on Save
	Again Click on Create Method
	Select POST Type
	Click on tick to create it.
	Integration type: HTTP
	Select Use HTTP Proxy integration
	Endpoint URL: http://springbootrestawsapigatewayexample-env.eba-u2izsrft.us-east-1.elasticbeanstalk.com/employees
	Click on Save
	Again Click on Create Method
	Select PUT Type
	Click on tick to create it.
	Integration type: HTTP
	Select Use HTTP Proxy integration
	Endpoint URL: http://springbootrestawsapigatewayexample-env.eba-u2izsrft.us-east-1.elasticbeanstalk.com/employees
	Click on Save
	Again Click on Create Method
	Select DELETE Type
	Click on tick to create it.
	Integration type: HTTP
	Select Use HTTP Proxy integration
	Endpoint URL: http://springbootrestawsapigatewayexample-env.eba-u2izsrft.us-east-1.elasticbeanstalk.com/employees
	Click on Save
	Click on Actions
	Click on Deploy API
	Deployment stage: New Stage
	Stage name*: prod
	Click on Deploy
	Now Under Stage click on prod
	Click on GET or Any Method you will find Invoke URL
	Invoke URL: https://3w4hjrtmw8.execute-api.us-east-1.amazonaws.com/prod/keshri-employee-service
	Use This URL in Postman Collection to Call the api or Use API Gateway itslf to Test the API

> Test the API
	Click on Resources
	Click on any method in API Gateway resource
	Click on Test
	Add if any query parameter needed
	Click on Test
	See the Result in the Gateway Itself with all the data and logs
	To Test Query param API under Query Strings
	id=3
	See Employee with id=3 as the Result in the Gateway
	
	
	
