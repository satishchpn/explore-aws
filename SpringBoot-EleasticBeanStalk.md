#Use ElasticBeanStalk
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
  
Download Spring boot Project(spring-boot-aws-example.zip). Unzip it and build jar file to later upload into Elastic BeanStalk.
  
> Note: Elastic Beanstalk is configured to forward requests to port 5000 by default so change the application port to 5000 if not there

    Open application.properties change server.port to 5000
    server.port=5000
    Open cmd and type mvn clean install to create spring-boot-aws-example.jar file
    
> Login to AWS account
    UN: cloud_user
    Password: <password>
			
> Note: Always make sure that you have selected AWS Region: US East (N. Virginia) us-east-1

> Navigate to Elastic Beanstalk Dashboard (AWS Region: US East (N. Virginia) us-east-1)
	
    Click on Create Application
    Application name: spring-boot-aws-example
    Platform: Java
    Platform branch: Choose appropriate Java version(Corretto 17)
    Application code: Upload your code
    Source code origin: Click on choose file
    Upload spring-boot-aws-example.jar
    Click on Create Application
    Wait to EC2 Instance get created and see Successfully launched environment: Springbootawsexample-env and Health as OK(Green)
    You will find the ec2 instance application url : http://springbootawsexample-env.eba-fuepzbxp.us-east-1.elasticbeanstalk.com/

> See the API Result In Browser
	
    http://springbootawsexample-env.eba-fuepzbxp.us-east-1.elasticbeanstalk.com/
    Hi Keshri - Welcome to AWS

    http://springbootawsexample-env.eba-fuepzbxp.us-east-1.elasticbeanstalk.com/home
    Welcome Keshri to First Spring Boot - AWS Deployment Demo

