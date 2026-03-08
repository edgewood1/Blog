
Here's a breakdown of the steps to get your website up and running on AWS with a CI/CD pipeline:
1. S3 Bucket hosts index.html:
	•	S3 Bucket hosts your app files.  
	•	Configuring S3: Enable static website hosting on the S3 bucket properties. You'll specify index.html as the index document (this is usually the default).
	•	You can also configure a custom error document in case requested page not found. 
	•	Check correct permissions 
	•	can only host static sites.  I can only server html, css, js.  Doesn’t support server side scripting or dynamic content generation  It has no server side processing. It can’t interact with databases, etc. 
2. Domain Name points to Bucket
	•	AWSRoute 53: this is amazon’s DNS service.  
	•	Use this to create records that point your domain name to the S3 bucket hosting your website.   

3. CloudFront (optional) 
	•	improves performance / global distribution. 
3. CI/CD Pipeline: GithubActions or AWS CodePipeline.
	•	allow you to automate the build and deployment process. As you develop your app and add more files, you'll just need to push them to your Git repository. The CI/CD pipeline will automatically pick up the changes, build if necessary, and deploy the updated website to your S3 bucket.
	•	Pipeline steps:   
	◦	Source: retrieves your code from your Git repository.
	◦	Build: build your site (like processing code or compiling assets) 
	◦	Deploy: uploads your built website files (including index.html) to the S3 bucket.
Hosting Dynamic Websites on AWS: Strategies and Data Flow
AWS Services for Dynamic Websites
While Amazon S3 excels at hosting static websites, you can leverage its capabilities alongside other AWS services to create dynamic web experiences. Several architectural patterns can be employed.  They are listed below 
The easiest approach for beginners is using Amplify.  Using it is an intro to Lambda, API Gateway, and CloudFront.  It also has a Database option: data store with app sync and dynamoDB is the most common.  You can also use GraphQL API: You can directly interact with your DynamoDB database using GraphQL queries and mutations through the AppSync API. REST API (with API Gateway & Lambda).  If you need more customization or want to use a different backend technology than DynamoDB, you can create a REST API using API Gateway and Lambda functions
The hardest is EC2.  
Learning Path Recommendation
	•	Start with Amplify: If you're a beginner, start with Amplify to build a solid foundation in full-stack development and serverless concepts.
	•	Explore Lambda and API Gateway: Once you're comfortable with Amplify, explore how to use Lambda functions and API Gateway to create more customized backend APIs and integrations.
	•	Leverage CloudFront: Learn how to use CloudFront as a CDN to improve performance and global distribution.   
	•	Consider EC2 (if needed): For highly complex or customized requirements, or if you need full control over your server environment, then consider venturing into EC2.
Architectural patterns
S3 + CloudFront + Lambda@Edge: Ideal for adding basic dynamic elements like user authentication, personalization, or A/B testing.  Good for Simple Dynamic Content / lightweight dynamic features.
	•	S3 stores the core static assets of your website (HTML, CSS, images).
	•	CloudFront, a Content Delivery Network (CDN), sits in front of S3 to accelerate content delivery and improve global reach.
	•	Lambda@Edge functions, triggered by viewer requests or responses, execute serverless code directly at CloudFront edge locations. This enables you to modify content, handle authentication, or perform other dynamic actions close to your users, reducing latency.
S3 + API Gateway + LambdaWell-suited for API-driven websites that heavily rely on backend data fetching and interactions.  Good for API-Driven Websites.

	•	Static assets reside in S3.
	•	API Gateway provides a fully managed service to create, publish, maintain, monitor, and secure APIs.It handles routing requests to the appropriate backend logic.
	•	Lambda functions process the API requests, interact with databases or other backend services, and generate dynamic responses.
Amplify: A great choice for full-stack web and mobile applications, offering simplified development and deployment.
	•	Features: Provides integrated services like authentication, database management, storage, and serverless functions, streamlining the process of creating dynamic websites.
EC2 (Virtual Servers): Offers maximum flexibility for complex or highly customized dynamic websites. How It Works:
	•	You launch EC2 instances (virtual servers) and install your preferred web server (e.g., Apache, Nginx) and backend technologies (e.g., Node.js, Python, Ruby).
	•	This gives you complete control over your server environment and allows you to implement any custom logic or integrations required for your website.
Data Flow in Next.js Dynamic Websites
Local Development:
	•	JavaScript functions in your Next.js application handle user interactions and make requests to your backend (e.g.,an Express.js server).
	•	The backend interacts with the database (e.g., PostgreSQL, MySQL) to fetch or update data.
Production (Two Options):
	1	Serverless Architecture (Lambda):
	◦	Next.js routes requests to API Gateway.
	◦	API Gateway triggers Lambda functions to handle the dynamic parts of your application.
	◦	Lambda functions interact with an external database (e.g., RDS or DynamoDB) to fetch or update data.
	2	Pre-rendered with Incremental Static Regeneration (ISR):
	◦	A build process (e.g., using GitHub Actions) fetches data from the backend API or database.
	◦	Next.js generates static HTML files using this data and stores them in an S3 bucket.
	◦	CloudFront serves these static files to users.
	◦	The revalidate property in getStaticProps allows for periodic re-generation of pages to keep the content fresh.
Database Options on AWS
	•	RDS (Relational Database Service):
	◦	Traditional relational database (e.g., MySQL, PostgreSQL).
	◦	Stores data in tables with rows and columns, enforcing relationships between data.
	◦	Suitable for structured data and complex queries.
	•	DynamoDB:
	◦	NoSQL database.
	◦	Offers flexible schema and scales easily for large datasets and high traffic.
	◦	Ideal for applications requiring fast and flexible data access.
Here are some resources to get you started:
	•	S3 Static Website Hosting: https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html
	•	Route 53 Hosted Zones: https://docs.aws.amazon.com/route53/
	•	AWS CodePipeline: https://aws.amazon.com/codepipeline/
	•	GitHub Actions: https://docs.github.com/actions
Here are some resources to get you started with dynamic website functionalities:
	•	Using GitHub Actions & Pages to Publish Static Pages Based on Dynamic Data:https://github.com/marketplace/actions/update-json-file-values
	•	Writable Websites using GitHub Pages + GitHub Actions: https://github.com/actions/runner/issues/1146
Appendix
AWS for beginniers / Vick Middleton // this is just a list

Ways to manage / access AWS services
	•	sending requests to API via we based GUI (management console)
	•	command=line interface (CLI) via terminal
	•	programmatically via an SDK

Creating an AWS account 
