
#Use Standalone Java - AWS Lambda
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
 
> Download Standalone Java Project Project(StandaloneAWSLambdaExample.zip). Unzip it and create jar out of it.
	
	Unzip StandaloneAWSLambdaExample.zip
	Import java application to Eclipse
	Right click on project
	Click on Export 
	Under Java select Jar File
	Click Next
	Click Next
	Click Next
	Browse and Select Main Class: com.keshri.aws.lambda.LambdaMain
	Click on Finish
	This will create StandaloneAWSLambdaExample.jar
	Use the jar to create the Lambda Function
	
 
> Navigate to Lambda Dashboard (AWS Region: US East (N. Virginia) us-east-1)

	Add a Lambda Function
	      Click on Create Function
	      Function name: EmployeeSupplier
	      Runtime: Java 11 Corretto
	      Click on Create function
	      Go to Code Section
	      Click Upload from
	      Select .zip or .jar file
	      Click on Upload
	      Select the application .jar file(StandaloneAWSLambdaExample.jar)
	      Click on Save
	      Click on Edit Runtime settings
	      Handler: com.keshri.aws.lambda.functions.EmployeeSupplier::get
	      Click on Save
	      
	Add another Lambda Function
	      Click on Create Function
	      Function name: EmployeeConsumer
	      Runtime: Java 11 Corretto
	      Click on Create function
	      Go to Code Section
	      Click Upload from
	      Select .zip or .jar file
	      Click on Upload
	      Select the application .jar file(StandaloneAWSLambdaExample.jar)
	      Click on Save
	      Click on Edit Runtime settings
	      Handler: com.keshri.aws.lambda.functions.EmployeeConsumer::accept
	      Click on Save

	Add another Lambda Function
	      Click on Create Function
	      Function name: EmployeeFunction
	      Runtime: Java 11 Corretto
	      Click on Create function
	      Go to Code Section
	      Click Upload from
	      Select .zip or .jar file
	      Click on Upload
	      Select the application .jar file(StandaloneAWSLambdaExample.jar)
	      Click on Save
	      Click on Edit Runtime settings
	      Handler: com.keshri.aws.lambda.functions.EmployeeFunction::apply
	      Click on Save
	      
> Navigate to API Gateway Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
	Click on APIs
	Click on Create API
	Click on Build Rest API
	Choose the protocol: Rest
	Create new API: New
	API Name: keshri-employee-api
	Click on Create API
	
	Click on Actions
	Click on Create Resource
	Resource Name: employee-get-service
	Click on Create Resource
	Click on Actions
	Click on Create Method
	Select GET Type
	Click on tick to create it.
	Integration type: Lambda Function
	Lambda Function: Select EmployeeSupplier
	Click on Save
	
	Again Click on Create Resource
	Resource Name: employee-getbyname-service
	Click on Create Resource
	Click on Actions
	Click on Create Method
	Select POST Type
	Click on tick to create it.
	Integration type: Lambda Function
	Lambda Function: Select EmployeeFunction
	Click on Save
	
	Again Click on Create Resource
	Resource Name: employee-add-service
	Click on Create Resource
	Click on Actions
	Click on Create Method
	Select GET Type
	Click on tick to create it.
	Integration type: Lambda Function
	Lambda Function: Select EmployeeConsumer
	Click on Save	
	
	Click on Actions
	Click on Deploy API
	Deployment stage: New Stage
	Stage name*: prod
	Click on Deploy
	Now Under Stage click on prod
	Click on Any Resource and Test it.
	
> Test the Resource
	
	Click on Resources
		Test EmployeeSupplier
		Click on GET method under employee-get-service resource
		Click on Test
		Click on Test
		It will return List of Employyes.
		
		Test EmployeeFunction
		Click on POST method under employee-getbyname-service
		Click on Test
		In Request Body Part add the firstName of Employee which you wated to get it. 
			"Sujit"
		Click on Test
		It Will add one Emploee to the List
		
		Test EmployeeConsumer
		Click on POST method under employee-add-service resource
		Click on Test
		In Request Body Part add below JSON
		
			{
			    "id": 5,
			    "firstName": "Test",
			    "lastName": "Saurabh",
			    "emailId": "saurabh@gmail.com"
			}
		Click on Test
		It will add one Employee to the List.
		

