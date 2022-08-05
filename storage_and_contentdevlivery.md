Storage & Database Services:
Amazon Simple Storage Service (Amazon S3) - scalable storage in d cloud

Amazon Simple Storage Service (Amazon S3) Glacier - archive storage in d cloud

DynamoDB - managed NoSQL db
Relational Database Service (RDS)
Redshift - fast, simple, cost-effective data warehousing
ElastiCache - in memory cache
Neptune - Fast, reliable graph db build 4 d cloud
Amazon DocumentDB - fully-managed MongoDB-compatible db service 

Vertical scaling: adding cloud componts e.g increasing memory size, 
cpu, storage etc
Horizontal scaling: adding more instances
Diagonal: both vertical and horizontal

S3 & S3 Glacier:
S3 Glacier is used for data that are not used for day to day activities eg audit report, archives and data retrival may take hours unlike S3 

You can enable Multi-Factor Authentication (MFA) Delete on an S3 bucket to prevent accidental deletions.
S3 Acceleration can be used to enable fast, easy, and secure transfers of files over long distances between your data source and your S3 bucket.

-: DynamoDB
DynamoDB is a NoSQL document database service that is fully managed. Unlike traditional databases, NoSQL databases, are schema-less. Schema-less simply means that the database doesn't contain a fixed (or rigid) data structure.

DynamoDB is serverless as there are no servers to provision, patch, or manage.

https://aws.amazon.com/getting-started/hands-on/create-nosql-table/


======================
-: Relational Database Service (RDS)
Relational Database Service (RDS)
RDS (or Relational Database Service) is a service that aids in the administration and management of databases. RDS assists with database administrative tasks that include upgrades, patching, installs, backups, monitoring, performance checks, security, etc.

Database Engine Support
Oracle
PostgreSQL
MySQL
MariaDB
SQL Server

Q: What doesn't RDS help with?
Ans: Accessing ur db via secure shell(SSH)

======================
-: Redshift
Redshift is a cloud data warehousing service to help companies manage big data. Redshift allows you to run fast queries against your data using SQL, ETL, and BI tools. Redshift stores data in a column format to aid in fast querying.

=======================
-: Why do we need content delivery in the cloud?
Content Delivery In The Cloud
A Content Delivery Network (or CDN) speeds up delivery of your static and dynamic web content by caching content in an Edge Location close to your user base.

Benefits
The benefits of a CDN includes:
low latency
decreased server load
better user experience

========================
-: Cloud Front
CloudFront is used as a global content delivery network (CDN). Cloud Front speeds up the delivery of your content through Amazon's worldwide network of mini-data centers called Edge Locations.

When a user requests content that you're serving with CloudFront, the request is routed to the edge location that provides the lowest latency (time delay), so that content is delivered with the best possible performance.

CloudFront works with other AWS services, as shown below, as an origin source for your application:

Amazon S3
Elastic Load Balancing
Amazon EC2
Lambda@Edge
AWS Shield

Cache control headers determine how frequently CloudFront needs to check the origin for an updated version your file.

The maximum size of a single file that can be delivered through Amazon CloudFront is 20 GB.

CLOUDFRONT CAN ALSO BE USED AS A SECURITY MECHANISM VIA IT PERMISSION SECTION

========================
-: Exercise: S3 & Cloud Front
NB: CloudFront, after caching, speeds up the delivery of content to your website

Step 1. Create S3 Bucket
Leave d bucket policy as it is(i.e No public access)
Enable Static website hosting under ppties tab and enter index.html

Step 2. Upload Object to Bucket
Note that the Bucket has not allowed public access, therefore, the Sample.html 
file cannot be accessed via its object URL, such as 
https://arabog-cloud.s3.amazonaws.com/sample.html

NB: use d `npm run build` folder content in case of a react app  

Step 3. Create CloudFront Distribution
S3 bucket accessInfo
Use a CloudFront origin access identity (OAI) to access the S3 bucket.
Origin Access Identity user represents the CloudFront service. The policy 
is a JSON file that defines the access permissions to the bucket object.

Origin domain: select d s3 bucket u created.
Origin path: leave blank
S3 bucket access: Yes use OAI (bucket can restrict access to only CloudFront)
Create new OAI(origin access identity)
Bucket policy: Yes, update the bucket policy
Viewer protocol policy: Redirect HTTP to HTTPS
Leave other as default

Cleanup:
Delete S3, cloudfront, 
https://d21nkuqzcxkysp.cloudfront.net/index.html
========================
