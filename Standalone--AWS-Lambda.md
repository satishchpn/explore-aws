
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

	      Now Click on Test Section
	      In Event JSON paste the below sample JSON
	      ""

	      Click on Test
	      It will return List of Employyes.
	      
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

	      Now Click on Test Section
	      In Event JSON paste the below sample JSON
		{
		  "id": 4,
		  "firstName": "Kumar",
		  "lastName": "Saurabh",
		  "emailId": "saurabh@gmail.com"
		}

	      Click on Test
	      It Will add one Emploee to the List
      
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

	      Now Click on Test Section
	      In Event JSON paste the below sample JSON
		"Satish"

	      Click on Test
	      It Will return one Employee whose firstName is Satish
