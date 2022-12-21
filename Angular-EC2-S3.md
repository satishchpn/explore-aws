# Use IAM , S3 , EC2
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

#Deploy Angular application to AWS
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Download Angular project(keshri-angular-demo.zip). Unzip and build to later place into aws s3 bucket.

	Go to project root directory in local
	Open cmd
	Type below command to build and generate production ready code
	npm install
	ng build --configuration production
	It will create dist folder with some files inside it, it will be used to deploy to AWS
	
> Navigate to S3 Dashboard (AWS Region: US East (N. Virginia) us-east-1)

	Use the bucket if you have already or create a new bucket
	
	Click on create Bucket		
		Bucket Name:keshri-bucket
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

		It will show List of Universities In India
