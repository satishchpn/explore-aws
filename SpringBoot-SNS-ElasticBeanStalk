
#Use ElasticBeanStalk - SNS(Simple Notification Service)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
 
> Navigate to SNS(Simple Notification Service) (AWS Region: US East (N. Virginia) us-east-1)

      Topic Name: keshri_topic
      Click on Next Step
      Select Standard Type
      Click on Create Topic
      Copy ARN URL of the Topic which will be used to connect to it.
      ARN: arn:aws:sns:us-east-1:768406036787:keshri_topic
      Now Get Access Key and Secret key to connect to the queue
 
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
        Access key ID: AKIA3F2ERUEZ2X2DZEGV
        Secret access key : kzKgP2Q6GHMfuS5HWvjDYRhdABODEhfujym8NGBQ
        Click on Close

Download Spring boot Project(spring-boot-aws-sns-example.zip). Unzip , Update the config and build jar file to later upload into Elastic BeanStalk.
  
> Note: Elastic Beanstalk is configured to forward requests to port 5000 by default so change the application port to 5000 if not there

    Open application.properties change server.port to 5000
    server.port=5000
    Update aws and sns config in properties file
    Open cmd and type mvn clean install to create spring-boot-aws-sqs-example file

> Navigate to Elastic Beanstalk Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
    Click on Create Application
    Application name: spring-boot-aws-sns-example
    Platform: Java
    Platform branch: Choose appropriate Java version(Corretto 17)
    Application code: Upload your code
    Source code origin: Click on choose file
    Upload spring-boot-aws-sns-example.jar
    Click on Create Application
    Wait to EC2 Instance get created and see Successfully launched environment: Springbootawssnsexample-env and Health as OK(Green)
    You will find the ec2 instance application url : http://springbootawssnsexample-env.eba-r7jpzmm3.us-east-1.elasticbeanstalk.com/
  
> Send some sample message through Browser
	
	Subscribe to The topic
		http://springbootawssnsexample-env.eba-r7jpzmm3.us-east-1.elasticbeanstalk.com/addSubscription/abc@gmail.com
		
	Confirm Subscrption
		Login to the given emailid and confirm subscription
		
	Send sample notification
		http://springbootawssnsexample-env.eba-r7jpzmm3.us-east-1.elasticbeanstalk.com/publish/test_notification
	
	Check Sent Notification in Email
