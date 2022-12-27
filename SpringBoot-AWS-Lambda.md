
#Use SpringBoot - AWS Lambda
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
 
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
	      Select the application .jar file(spring-boot-aws-lambda-example.jar)
	      Click on Save
	      Click on Edit Runtime settings
	      Handler: com.keshri.aws.lambda.functions.EmployeeSupplier::get
	      Click on Save

	      Now Click on Test Section
	      In Event JSON paste the below sample JSON
	      ""

	      Click on Test
	      
	Add another Lambda Function
	      Click on Create Function
	      Function name: EmployeeConsumer
	      Runtime: Java 11 Corretto
	      Click on Create function
	      Go to Code Section
	      Click Upload from
	      Select .zip or .jar file
	      Click on Upload
	      Select the application .jar file(spring-boot-aws-lambda-example.jar)
	      Click on Save
	      Click on Edit Runtime settings
	      Handler: com.keshri.aws.lambda.functions.EmployeeConsumer::accept
	      Click on Save

	      Now Click on Test Section
	      In Event JSON paste the below sample JSON
		{
		  "id": 4,
		  "firstName": "Kumar",
		  "lastName": "Saurabh",
		  "emailId": "saurabh@gmail.com"
		}

	      Click on Test
      
      Add another Lambda Function
	      Click on Create Function
	      Function name: EmployeeFunction
	      Runtime: Java 11 Corretto
	      Click on Create function
	      Go to Code Section
	      Click Upload from
	      Select .zip or .jar file
	      Click on Upload
	      Select the application .jar file(spring-boot-aws-lambda-example.jar)
	      Click on Save
	      Click on Edit Runtime settings
	      Handler: com.keshri.aws.lambda.functions.EmployeeFunction::apply
	      Click on Save

	      Now Click on Test Section
	      In Event JSON paste the below sample JSON
		"Satish"

	      Click on Test

	Add another Lambda Function
	      Click on Create Function
	      Function name: EmployeeSupplier
	      Runtime: Java 11 Corretto
	      Click on Create function
	      Go to Code Section
	      Click Upload from
	      Select .zip or .jar file
	      Click on Upload
	      Select the application .jar file(spring-boot-aws-lambda-example.jar)
	      Click on Save
	      Click on Edit Runtime settings
	      Handler: com.keshri.aws.lambda.functions.EmployeeSupplier::get
	      Click on Save

	      Now Click on Test Section
	      In Event JSON paste the below sample JSON
	      ""

	      Click on Tet
