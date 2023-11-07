
# Deplyoing Static Website on S3 Bucket with CI/CD(GitHub Actions)

## A functional example of hosting simple website on S3 Bucket with help of CloudFront Distribution and Deplyoing CI/CD Pipeline using GitHub Actions

This project is an example of hosting static website on S3 Bucket and using CloudFront Distribution that is CDN service that securely delivers data, videos, applications, and APIs to customers globally with low latency. We will used GitHub Actions to create workflows that build and test every pull request to your repository, or deploy merged pull requests to production.


* Create a S3 Bucket and Upload your Website files
* Create a CloudFront Distribution using S3 Bucket as Origin
* Create new repository in GitHub and sync it with your local repository(Website)
* Now create .github/workflows directory to your repository
* In that directory we will define our workflow in YAML file
* Now make change in repository and commit and push the changes
* Check the GitHub Actions Tab in your repository and Deploy the job

## Detailed Process and Cautions:

### Sample Code and Local Repository Creation:

* Create folder with Project name where it will be easy to navigate the files and suitable to handle

* Noe create index.html file in that folder and write some sample Code in it. For Reference I used this Code. Link: https://www.w3schools.com/howto/tryit.asp?filename=tryhow_css_profile_card

* You can also use code of your choice and use GitHub Actions to commit and push new changes to it automatically.

### S3 Bucket Creation:

* Create S3 Bucket from https://s3.console.aws.amazon.com/s3/home?region=ap-south-1  You can change Region/Zone(ap-south-1) also as per your requirement or preference as I have used Mumbai Region here.
* Caution: While creating S3 Bucket is that make sure you access to Block Public Access settings for this bucket is set to --> Bucket and objects not public. Because you don't want third party to access it.


### CloudFront Distribution:

* Now open the CloudFront service tab Link: https://us-east-1.console.aws.amazon.com/cloudfront/v4/home?region=ap-south-1#/distributions/create (Make sure to check zone since it is link to Mumbai Region)

* On Creation page select Origin Domain as your S3 Bucket

* Set Origin Access as "Origin Access as Control Settings (recommended)" under that option there will be option to select configuration which comes under "origin access control" and click on "Create control setting". It will be pre-configured already just click on Create.

* Now we are done with most part. Next up under settings in Viewer Protocol select: HTTPS Only and make sure Web Application Firewall(WAF) is disabled. 

* Now just Create the Distribution.

* When distribution is created go to the distribution and in General Tab scroll down you will find settings option and click on Edit. There in Default Root Object put index.html as your root object. If you don't then it will display error.

* When you create distribution you will need to update Bucket Policy which will displayed to copy to your clipboard or you can just access it using setting from distribution Menu. Go to S3 section and switch to your bucket and navigate to Permissions tab  and if you scroll down you will find policy option just edit and paste it there.


### GitHub Part:

* Go to your Local Repository and open it in Visual Studio Code. Launch the terminal on it. Now configure the Git Init and sync it with your GitHub Repository. Or alternative you can use Git Bash 

* Now create new folder in that Repository ".github" make sure extention is right. In ".github" folder add another folder named "workflow" and create YAMl file with name of your choice in workflow folder. Now you can take code from my Repository which included in same directory.

* Now make some changes in your code and commit the changes and push the code to origin. Or just commit with visual code source control and click on Sync.

* Open your GitHub Repository and go to Actions tab and open "Upload Website to S3 bucket" workflow and you will see there is new change pending to deployed. Just click on "Deploy". Now workflow will be start and when it gets completed you can refresh the site and check if changes are done. 

* Cauations: If you don't find the changes being made on your site just know that the cache content with CloudFront Distribution doesn't get refreshed instantly since it is by default set to 24H. So just go to CloudFront and navigate to your distribution and you will see Invalidate tab and click on it and create it and just type index.html in displayed pop up.