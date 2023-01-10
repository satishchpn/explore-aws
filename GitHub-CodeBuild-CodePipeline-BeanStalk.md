#Use Spring Boot , GitHub , CodeBuild , CodePipeline , Elastic BeanStalk
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Create Spring boot Project(keshri-spring-boot-aws-crud-demo) in GitHub(https://github.com/satishchpn/keshri-spring-boot-aws-crud-demo)
	
> Login to AWS account

	UN: cloud_user
	Password: <password>
	
> Note: Always make sure that you have selected AWS Region: US East (N. Virginia) us-east-1

> Navigate to Elastic Beanstalk Dashboard (AWS Region: US East (N. Virginia) us-east-1)

	Click on Create Application
	Application name: keshri-spring-boot-aws-crud-demo
	Platform: Java
	Platform branch: Choose appropriate Java version(Corretto 17)
	Application code: Sample code
	Click on Create Application
	Wait to EC2 Instance get created and see Successfully launched environment: Keshrispringbootawscruddemo-env and Health as OK(Green)
	You will find the ec2 instance application url : http://keshrispringbootawscruddemo-env.eba-5y3qb4p3.us-east-1.elasticbeanstalk.com/

> Navigate to CodePipeline (AWS Region: US East (N. Virginia) us-east-1)

	Click on Create Pipeline
	Pipeline name: keshri-demo-pipeline
	Click on Next
	Select Source provider: GitHub(Version 1)
	Click on Connect to GitHub
	Grant the Access
	Select Repository: satishchpn/keshri-spring-boot-aws-crud-demo
	Branch: main
	Click on Next
	Build provider: Select AWS CodeBuild
	Region: US East (N. Virginia)
	Click On Create Project
	Project name: keshri-demo-project
	Operating system: Amazon Linux 2
	Runtime(s): Standard
	Image: choose latest one(4.0)
	Click on Continue CodePipeline
	Click on Next
	Deploy provider: Elastic BeanStalk
	Application name: Choose keshri-spring-boot-aws-crud-demo
	Environment name: Keshrispringbootawscruddemo-env
	Click on Next
	Click on Create Pipeline
	After Succesful Deployment Test the API 
	Use http://keshrispringbootawscruddemo-env.eba-5y3qb4p3.us-east-1.elasticbeanstalk.com/ in  Postman Collection to test the APIs
	
