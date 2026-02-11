Server is composed of Compute(CPU). Memory(RAM), Storage(Data - 010101), Database(Structured way), Network(Router, switch, DNS Server).



Problems with traditional IT

Pay rent for data center, power supply, maintenance.

Adding, replacing hardware takes time.

Scaling is limited.

Need to monitor 24/7.

Cloud can externalize all these.



CC is on demand delivery with pay as u go model(***pricing model)***.

Delivers Compute, Database, applications.

AWS owns and maintains the n/w connected hardware req for application services while we provision and use what we need via web application.



##### Deployment models:

Private Cloud: C Services used by a single org, not exposed to public - complete control - meet specific business needs

Public C: Owned and operated by third party cloud services.

Hybrid: keep some servers om premises and extend some capabilities to cloud -  control over some private assets in our pvt infra.



Trade Capital Expense(CAPEX) for operational expense(OPEX) - pay on demand, dont own hw.

Can go global in min.

Flexibility, Scalability, Elasticity, High avai, Fault tolerance, Cost effective, agility.



Types - SAAS, IAAS, PAAS

IAAS - EC2

PAAS - Beanstalk

SAAS - Gmail



AWS has ***3 pricing fundamentals*** following pay-as-you-go pricing model

Compute - pay for compute time

Storage - Pay for data stored

Data transfer out of the cloud as IN is free.



##### AWS Global Infra:

Regions - all around world - US-East-1 - Cluster of Data Centers

Factors to choose Regions - Compliance with data governance, Proximity to customers, Available services within the region(new ftrs are not av in every region), Pricing

AZs - inside region - each reg has min 3, max 6 AZs - US-East-1a  -  each AZ is one or more discrete data centers with redundant powers, nw. Isolated from each other to avoid disaster. These are connected with high bandwidth, utra-low latency nwing

Data Centers

Edge Locations/ Points of Presence - 400+ POPs, 10+ regional caches. Content is delivered to end users with low latency.

All the above are Global Infra Identity



##### Global Services:

IAM, Route 53(DNS Service), CloudFront(Content Delivery NW), WAF(Web App Firewall)

Region Scoped:

EC2, Beanstalk, Lambda(FAAS), Recognition(SAAS)



AWS Shared Responsibility Model:





##### Security Group

Inbound Rules - http tcp 80 anywhere  0.0.0.0/0 allows to view an EC2 instance(in web browser)

Timeout error occurs for sec group misconfiguration

Outbound rules - ipv4 all traffic - used to give access of full connectivity anywhere to our EC2 instance

Need ssh 22 anywhere - to connect ti instance from any of the 4 methods after hitting connect





##### EBS

EBS are network drives which are attached to the instance - data persists even after inst is terminated. (Think of it as a pen drive)

Root volume - delete on termination enable by def(attribute enabled) - can also check in instance's storage settings - delete on termination enabled.

EBS volume - delete on termination disabled by def(attribute disabled (exam)

EBS volumes can be connected to one instance at a time but single inst can have multiple volumes connected to it.

EBS volume are AZ specific - can be attached to EC2 instances present in respective AZ

Snapshot is a backup of our EBS Volume, used to transfer EBS volumes across AZs.

Not necessary to detach volume while snapshot - but recommended

EBS snapshots are stored in regions - helps to move across AZs

Possible to copy across regions too

EBS Snapshot archive - vd 53

Recycle bin for EBS snapshots - vd 53



Eg for moving vol across AZ

Create vol in us-east-1a -- create its snapshot - go to snapshots - create volume from snapshots - choose us-east-1b - done

Vd 54 - revision - recycle bin



###### EC2 Instance Store

EBS Volume....

Better I/O performance.

EC2 Instance store lose their storage if stopped(ephemeral).

Used for buffer, cache, temp content, scratch data



##### AMI

AMI are a customization of an EC2 instance.

We add our own sw, config, os, monitoring while creating an instance and create its AMI - later we can launch an instance from this AMI without configuring again.

Helps to add your own sw license

Faster boot/conf time as all our software is pre packed.

2 types of launching instances from AMI - from ami section, while launching new instances -> select ami from my amis.

Example:

Create an instance -> in user's data -> yum update -y, yum install httpd -y, systemctl start httpd, systemctl enable httpd. -> launch instance

Create its AMI. Launch new instance from this AMI. In user's data -> echo "hello" > /var/www/html/index.html.

Do not need to write again in this instance regarding httpd config as it is already present in the AMI from which the new instance is created.

AMI are region specific.

Public AMIs, Own AMIs, AWS Marketplace AMIs(third party's AMI)

Public AMI vs Own AMI vs AWS Marketplace AMI.

56 - rev



##### EC2 Image Builder

Automatically build, test and distribute AMIs.

Automates image management process.

Used to automate the creation of VMs or container images.

Automates the creations, maintain, validate and test EC2 AMIs.

Can be run on a schedule. Free service.

EC2 IB -> Builder EC2 Inst -> New AMI -> Test EC2 Inst -> AMI is distributed(multiple regions).



##### Elastic File System

Managed *Network file system*, can be mounted on 100s of EC2

EFS works with Linux EC2 instances in multi-AZ.

High av, sc, expensive, pay per use, no capacity planning.



EBS vs EFS

EBS allows snapshots.

EFS mounts data on all AZs in a shared manner. (shared file system).



EFS-IA - google

EFS IA is a file system)cost-optimized storage class) to which files are moved if unused for a long time.

It stores infrequent accessed files



##### Shared Responsibility of EC2 Storage.

AWS manages:

Infra

Replication of data for EBS vol and EFS drives.

Replacing faulty hw.

Zero-day.



User manages:

Setting up backup/ snapshot procedures.

Setting up data encryption.

Responsible for any data on drives.

Understanding the risk of using EC2 instance store.



##### AWS FSx (File System)

Fully Managed service to get high performing file systems on AWS if we do not want to use EFS or S3.

###### *FSx for windows file server:*

Fully mamaged native Microsoft Windows file system.

NFS for Windows Server.

Built for Windows file server.

Supports SMB protocols and Windows NTFS.

It is highly reliable and scalable Windows native shared file system.

Can be accessed from AWS or on premise.

###### *FSx for Lustre:*

High Performance Computing(HPC) Linux file system

Lustre - Linux + Cluster

FMged, high-perf, scalable file storage for High Performance Computing(HPC).

ML, Analytics, Video processing, financial modelling.

Scales upto 100s GB/s, millions of iops, sub-ms latencies.



Vd - 64

##### Vertical Scalability

Inc size of instance from t2.micro to t2.small.

Common for non distributed systems such as database.

Limits present on how much we can scale(hw limit).



##### Horizontal Scalability

Inc no of instances.

Implies distributed systems.

Common for web apps/ modern apps.

AWS EC2.



*High av* means app is running in at least 2 AZs.

Helps to survive data loss.

High av goes hand in hand with Hor Sca.



Scalability means ability to accommodate larger load by making hw stronger(scale up), or by adding nodes(scale out).

Elasticity means, once a system is scalable there will be some auto scaling.

Agility means reducing time to make those resources available.



##### Load Balancers

Load Balancer are servers that forward internet traffic to multiple servers.

Helps to spread load.

Exposes single point of access(DNS) to your app.

Does regular health checkups of our inst.

LBs cannot help with back-end autoscaling, for this we need ASGs.

Provide SSL termination for our websites.

ELB is a managed LB.

AWS takes care of it.

4 types of LB:

Application LB: Http/https only, gRPC protocol, static DNS(URL) - layer 7

Network LB: allows tcp/udp/tls, static ip through elastic ip, high performance, low latency, millions of equests for sec - layer 4

Gateway LB: GENEVE Protocol on IP packets, Routes traffic to firewalls that are managed on EC2 instances, intrusion detection - Layer 3

Classic LB: retires in 2023: Layer 4 and 7.

Practical - Vd 66

Sec group is needed for a load balancer.

Load is forwarded/directed to target groups(group of instances) under listeners and routing while creating load balancer.

DNS name of the LB is used to get the data which is distributed in diff instances through LBs



##### Auto Scaling Groups

Scale out and scale in to match the incoming load.

Automatically register new instances to a load balancer.

Replaces unhealthy inst.

Ensures we have a min/max no of running inst.

Min size - Actual size/ Desired Capacity - Max size.

ASG works hand in hand with LBs.

ASGs can add or remove instances, but from the same type, cannot change instance type on the fly.

Eg of Horizontal scaling as it adds instances.

Prac - vd 68 - not done



ASG scaling strategies:

Manual scaling: manual

Dynamic scaling: responds to changing demand, cpu usage wise(simple/step scaling)

: Target Tracking scale - we want ASG CPU to stay around 40%

: Scheduled scaling

: Predictive scaling - ML oriented - uses past loads





##### AWS S3

Used for backup and storage

Disaster, Recovery, Archive

Hybrid Cloud Storage

Application hosting, media hosting, data lakes, big data analytics

SW delivery

Static website

S3 stores objects(files) in buckets(directories).

Buckets have globally unique name(across all reg and all accounts).

Buckets are defined at the region level.

No uppercase, underscore, no ip, not starts in prefix xn--, not ends with suffix -s3alias.

Objects have keys.

Key is the full path - key = prefix + object name.

There is no concept of directories within buckets even if UI will trick you.

Max obj size - 5TB - 500GB

If uploading > 5GB, must use "multi-part upload"

Metadata (list of text key/value pairs).

Tags used for security.

Version id.

Public URL is for public, another url(top right with open tag) is for creator itself(pre-signed url) - only creator can see the content of the object.

S3-security:

User based:

IAM policies - which API calls should be allowed for a specific user from IAM.

Resource based:

Bucket Policies - bucket wide rules from the s3 console - allows cross account.

Object ACLs - finer grain (can be disabled).

Bucket ACL - less common(can be disabled)

Vd - 74 - some left

Amazon Resource Name(ARN) in policy should be the bucket name

***AWS S3 - static website hosting***

We have to make sure the bucket policy allows public read otherwise we will get 403 forbidden error.

VD 77 - revision for static website hosting.

eg: go to buckets -> properties -> scroll down -> edit static website hosting -> enable -> index.html input -> go to objects -> upload your own index.html file -> go to properties -> under static website hosting -> you will get the link.

Versioning -> enables at bucket level -> protects unintended delete -> easy rollback to previous version -> suspending versioning does not delete the previous version.

Versioning helps to create version of files when we overwrite any file.

eg: u have an index.html file, go to properties -> enable versioning -> again upload index.html with new content -> show versions will be present.

Deleting objects without versioning adds delete marker added to them by def -> can see after enabling show versions.

IF YOU DELETE THE DELETE MARKER, YOU WILL GET YOUR OBJECT BACK.(vd 79)

*AWS Cross region replication and same region replication*

Must enable versioning, copying is asynchronous

CRR - compliance, lower lat, repli across accounts

SRR - log aggregation, live repli bet prod and test accounts

Prac of replication - vd 81

S3 Storage classes - google

Durability and availability in S3

Storage class is available under properties while uploading objects.

Can change storage class in properties.

Lifecycle rule(under management attribute of bucket) - lifecycle setting after certain days.

S3 encryption - server-side enc (by default)

 		client side enc - user encrypts file before uploading it

IAM Access Analyzer for S3 ensures only intended people have access to your S3 buckets, eg: publicly accessible buckets, bucket shared with other AWS acc

Shared Responsibility:

AWS: Infra, config, compliance validation, vulnerability analysis, durability, availability, sustain concurrent loss of data in two facilities.

User: Versioning, bucket policies, replication setup, logging, monitoring, storage class, data enc at rest and in transit

AWS snow family hands on - vd 89 - revision

Snowball edge pricing:

Data transfer IN to Amazon S3 in 00 per GB.

Block Storage - Amazon EBS, Instance store

File - EFS

Object - Amazon S3, Glacier

AWS storage gateway is a bridge between on-prem data and cloud data.

Hybrid storage service to allow on-prem to seamlessly use the AWS cloud.

Used in disaster recovery, backup, restore, tiered services.

Types of storage gateway:

File, Volume, Tapes > AWS SG > EBS, S3, Glacier.



##### Databases (skipped)

Relational db:

Like excel spreadsheets, with links between them.

SQL is used

NoSQL db:

non relational

Flexible schema for modern apps.

Flexibility, scaling, highly functional

eg: key-value, graph, document, in-memory, search db.

In JSON format

Data can be nested.

Fields can change over time.

Supported for new types: arrays, etc.



Shared Responsibility:

OS patching is handled by AWS

AWS manages monitoring, alerting

Rest part at end.



Section 10

Docker

ECS - Elastic container service

Launches Docker cont on AWS.

WE provision and maintain the infra.

AWS takes care of starting and stopping containers.

Has integrations with ALBs.



Fargate:

Launch Docker cont on AWS

We di not provision infra.

Serverless.

AWS just runs cont for us based on CPU and RAM we need.



ECR - Elastic Container Registry

Private docker registry

This is where we store our images so they can be run by ECS or Fargate.



EKS - Elastic Kubernetes Service

Allows to launch managed Kubernetes clusters on AWS.

Can be hosted on EC2 instances, fargate.



Serverless

Developers don't manage servers

Only manage code

Initially it was FAAS, now it also includes anything that is managed: "databases, messaging, storage, etc."

Eg: S3, DynamoDB, Fargate(we just send docker conts, it finds a way to run them), Lambda(runs functions in cloud), Amazon API Gateway.



AWS Lambda:

EC2 are virtual servers in cloud.

Limited by RAM, CPU.

Continuously running.

Scaling means intervention to add more servers.

Lambda:

Virtual functions, no servers to manage.

Limited by time - short executions

Run on-demand.

Scaling is automated.

Lambda scales seamlessly.

Pay per request and compute time.

Event driven - function gets invoked by AWS when needed.

Integrated with many prog langs.

Easy monitoring through cloudwatch.

ECS, fargate is preferred to run contaners.

Lambda is Used in Serverless CRON Job - cloudwatch events eventbridge triggers every 1 hour to AWS lambda function to perform a task.

Lambda hands on - vd 117



Amazon API Gateway(Serverless API):

Building a serverless API.

Fully managed service for developers to easily create, publish, maintain, monitor and secure APIs.

Serverless and scalable.

Supports RESTful APIs and WebSocket APIs.



AWS Batch:

Fully managed bathc processing at any scale

It has a start and an end.

Batch dynamically launches EC2 instances or Spot Instances.

Batch provisions right amount of compute and memory.

Batch jobs are defined as Docker images and run on ECS.



Batch vs Lambda

Lambda has time limit, limited runtimes, limited temp disk space , serverless.

Batch has not time limit, any runtime, rely on EBS, relies on EC2 - not serverless.



AWS Lightsail:

Virt serv, storage, dbs, nw in one place.

Low and predictable price.

Simpler alternative to EC2, RDS, ELB, EBS, Route 53.

Used in simple web apps, dev/test environment.

Has high av, no auto scaling, limited AWS integrations.

Helpful for no cloud experience.

Prac - vd 121.





CloudFormation

Declarative way of outlining our AWS Infra for any resources.

Within a CF template, we say -

we want a SG, 2 EC2 inst, S3 bucket, ELB.

CF creates those for us in right order with the exact config we say.

IAC.

No resources are manually created.

Could automate deletion of templates at 5pm and recreate at 8am.

Ability to destroy and recreate an infra on the cloud on the fly.

Eg: WordPress CloudFormation Stack.

Used in repeating architecture in diff env and diff regions.

Handson - vd 124



AWS Cloud Development Kit(CDK):

Define your cloud infra using a familiar lang - python, java, etc.

A developer would like to deploy infrastructure on AWS but only knows Python. Which AWS service can assist him?

Code is compiled into a CF template(YAML/JSON).

We can deploy infra and application runtime code together.

Great for lambda func, Docker cont in ECS/EKS.



Elastic Beanstalk - developer centric view of deploying an app.

EBS uses all components  we've seen before - EC2, ASG, ELB, RDS, etc.

EBS is PAAS.

We only pay for underlying instances.

AWS manages inst config, OS, LB, AS, health monitoring.

App code is responsibility of user.

3 architecture models:

Single inst deployment: good for dev

LB + ASG: for production and pre-production web apps.

ASG only: great for non-web apps in prod(workers).

EBS has health agent which pushes metrics to CloudWatch.

Hands-on - vd 127



AWS CodeDeploy

Deploys our application automatically.

Works with EC2 inst and on-premise servers - hybrid service.

Servers/Instances must be provisioned ahead of time with the CodeDeploy agent.

Used in upgrading.



AWS CodeCommit

Storing purpose (code storing).

Similar to GitHub.

Hosts git based repos.

Collaborative.

Fully managed, scalable, high av, private, secured, integrated with AWS.



AWS CodeBuild

Compiles source code, runs tests, produces packages ready to be deployed.

Fully managed, serverless, secure, pay as u go - only pay for build time, scalable, high av.



AWS CodePipeline

Connects CC and CB.

Orchestrate diff steps to have the code automatically pushed to production.

Code - Build - Test - Provision - Deploy.

CC -> CB -> CD -> EBS  - this workflow is the orchestration layer of CP.

Orchestration of Pipeline - AWS CP



AWS CodeArtifact

Artifact Management System.

SW packages depend on each other to be built.

Storing and retrieving these dependencies is called artifact management.

Secure, scalable.

Works with dependency management tools like Maven, Gradle, npm, yarn, etc.

Developers and CodeBuild retrieve artifacts from CA.

###### 

AWS System Manager

Helps to manage EC2 and on-premise systems at scale.

Hybrid.

Suite of 10+ products.

Patching automation for enhanced compliance.

Run commands across an entire fleet of servers.

Runs a command consistently across all our servers.

Need to install SSM agent onto the systems we control.

We can run commands, patch and configure our servers.



AWS Session Manager

Allow us to start a secure shell on our EC2 and on-prem serv

No SSH access, SSH keys needed.

No port 22 needed

Sends session log data to S3 or CloudWatch logs.

Hands-on vd 134



System Manager Parameter Store

Secure storage for config and secrets.

API keys, pws, configs

Serverless, scalable, durable, easy SDK

Control access permissions using IAM

Version tracking and encryption



Global Application

App deployed in multi geographies.

Regions or edge locations.

Decreased latencies and Disaster Recovery.

Attack Protection.



AWS Global Infra

Regions - AZs - Edge Locations



AWS Route 53

Managed DNS.

DNS is a collection of rules and records which helps clients understand how to reach a server through URLs.

ipv4, ipv6.

Common records:

www.google.com -> ipv4 = A record

www.google.com -> ipv6 = AAAA

hostname to hostname = CNAME

example.com -> AWS resource = ALIAS (eg: ELB, CloudFront, S3, RDS, etc)

Exam perspective

Simple Routing Policy - no health checks

Weighted Routing Policy - weight is assigned to apps like the weight(70%) traffic will be on that server. Health checks are present.

Latency Routing Policy - Route 53 minimizes latency by making content available to customer from nearest edge location. Health checks present

Failover Routing Policy - has health checks, helps in disaster recovery.

Hands on - vd 139

In value attribute, we provide ip.

Eg: in R53, we add 2 records with routing policy - latency,

In value, we give ip of Ireland instance and US instance respectively in 2 diff records,

In created domain(one which we will create in R53) - Data will be provided based on proximity of the user and the location of server(Ireland or US),

If user is in Ireland - ip will be of instance in Ireland and same with US user - US ip,

Both have same data, only diff servers which are present in diff places, used to reduce latency.



CloudFront is a CDN - caches data for repeated delivery without fetching from the origin more than once(caching)

SS taken.

Prac - vd 141



S3 Transfer acceleration:

Inc transfer speed by transferring file to an AWS edge location which will fw the data to the S3 bucket in the target region.



AWS Global Accelarator:

Improve global application av and performance using AWS global nw.

Leverages AWS internal nw to optimize the route to our apps.

Continue from vd 143



AWS GA vs CloudFront

Both use AWS Global network and its edge location around the world.

Both integrate with AWS Shield for DDoS protection.

 CF - content is shared at the edge

 GA - no caching, proxying packets at the edge to app running on one or more AWS regions.

 GA is good for http and https use cases.

 GA improves performance for a wide range of apps over TCP or UDP.



AWS Outposts:

These are server racks that offers the same AWS infra, services, APIs and tools to build our own apps on-premise just as in the cloud.

AWS will setup and manage the Outposts Racks.

We are responsible for Outposts Rack physical security.

Benefits: Low latency to on prem systems

Low data processing

Data residency

Easy migration from on prem to cloud

Fully managed service.

Services that work on Outposts

EC2, EBS, S3, EKS, ECS, RDS, EMR



AWS WaveLength:

Infra deployment, embedded within the telecommunications providers' datacenters at the edge of the 5G nw.

Brings AWS services to the edge of the 5G nw.

EC2, EBS, VPC.

Wavelength Zone - google.

Ultra low latency through 5G nw.

Traffic does not leave the communication Service Provider's (CSP) nw.

High bandwidth and secure connection to the parent AWS region.

No additional charges or service agreements.

Use cases: Smart cities, ML assisted diagnostics, Connected vehicles, AR/VR, Real time gaming.



AWS Local Zones (Exam)

Places AWS compute, storage, db, and other selected AWS services closer to end users to run latency-sensitive apps.

Extends our VPC to more locations - extension of an AWS region.

Compatible with EC2, RDS, ECS, EBS, ElasticCache, Direct Connect.

Eg: AWS Region: N.Virginia(us-east-1), AWS Local Zones: Boston, Chicago, Dallas.

Zone Group - Google

EC2 Dashboard - account attributes in right - settings

Need to enable, then it will appear in AZs while creating a subnet.



Global Application Architecture:



Single R, Single AZ

High av not possible.

Global latency not possible

Difficulty



Single R, Multi AZ

High av

Global latency np

Difficulty moderate



Multi Region, Active-Passive

2 reg - each with >1 AZs

read/write in active

read in passive

Google

Global Reads' latency

Global writes' latency not possible

diff moderate



Multi R, Active-Active

2 reg - each with >1 AZs

read-write in both the servers

Global Reads' latency

Global writes' latency

diff moderate

vd 147 - rev



Cloud Integrations:

When we deploy multiple apps, they will need to communicate with each other.

2 patterns of app communication -

Synchronous - app to app

Async - app to queue to app

Sync -problem occurs when there is a sudden spike,

in this case it is better to decouple our apps using SQS queue model, SNS - pub/sub model, Kinesis - real time data streaming model,

These services can scale independently from our apps.



SQS:

Amazon Simple Queue Service

Producer sends msg to SQS queue, queue polls messages to consumer.



SQS Standard queue:

serverless - used to decouple apps

Scales from 1 msg per second to 10,000 per sec.

Msgs are deleted after they are read by consumers, low latency, no msg limit, consumers share the work to read msgs and scale hori.

SQS is used to decouple between app tiers.

Multiple producers - msgs are kept up to 14 days.

Multiple consumers share the read and delete msgs when done

Google for example.

SQS FIFO Queue:

SQS - FIFO - first in first out queue:

sent messages in 4-3-2-1 order -- consumer will read it in similar order(exam).

Messages are processes in order by the consumer.

Prac - vd 151.



Amazon Kinesis Data Streams:

Kinesis - real time big data streaming, persistence and analysis

Managed service to collect, process and analyse real time streaming data at any scale.

Amazon KDS

Amazon Data Firehouse (can ignore for this exam)



Amazon SNS: (notification, subscribe, publish)

Pub/Sub

Simple Notification Service

No message retention

Event publishers only sends message to one SNS topic

Each subscriber to the topic will get all the msgs.

SNS publishes to Subscribers(SQS, Lambda, Amazon Data Firehouse, Emails, SMS, Mobile noti, HTTP(S) Endpoints).

Prac - vd 154

SQS and SNS are cloud native services.



Amazon MQ:

Managed message broker for ActiveMQ and RabbitMQ in the cloud (MQTT,AMQP..protocols)

 It is a managed broker service for Rabbt MQ.

It runs on servers, can run in multiple AZ with failover.

Doesn't scale as much as SQS and SNS.

It has both queue features - SQS and topic features SNS.



##### **Machine Learning:**

Amazon Rekognition:

Find objects, people, text, scenes in images and vdos using ML.

Facial analysis and facial search to do user verification, people counting.

Labelling, Celebrity recognition, pathing(for sports game analysis).



Amazon Transcribe:

Converts speech to text.

Uses deep learning processes called Automatic Speech Recognition(ASR) to convert quickly and accurately.

Automatically remove Personally Identifiable Info(PII)(hides if there is name and number) using Reduction.

Supports Automatic Language Identification for multi-lingual audio.

Uses cases:

transcribe customer service calls, automate closed captioning and subtitling, generate metadata for media assets to create a fully searchable archive.

Auto language identification.



Amazon Polly:

Turns text into lifelike speech using deep learning.

Allowing us to create applications that talk.



Amazon Translate:

Neutral and accurate language translation.

Allows to localize content - websites, etc.

A company would like to convert its documents into different languages, with natural and accurate wording. What should they use?



Amazon Lex and Connect:

Lex is the same tech that powers Alexa.

Automatic Speech Recog)ASR.

Natural Language understanding to recognize the intent of text, callers.

Helps build chatbot, call center bots.

Connect receive calls, create contact flows, cloud based virtual contact center.

Mobile -(Call)- connect -(streams)- lex(intent recognized) -(invoke)- lambda -(schedule)- CRM.

A company would like to implement a chatbot that will convert speech-to-text and recognize the customers' intentions. What service should it use?



Amazon Comprehend:

For Natural Language Processing -NLP

Fully managed and serverless.

Finds meaning and insights in text.

A research team would like to group articles by topics using Natural Language Processing (NLP). Which service should they use?

Uses ML to find insights and reln in text - language of text, positive/negative, analyses text using tokenization, automatically organizes a collection of text files by topic.

Sample use cases:

Analyse customer interactions(email) to find what leads to positive or negative exp.



Amazon SageMaker AI:

F Managed serv for developers/data scntsts to buils ML models.

Diff to do all processes in one place + provision servers.



Amazon Kendra: (ML powered search-engine)

FM document search service powered by ML.

Extract ans from within a document(text, pdf, ppt, etc)

Natural Language search capabilities.

Incremental learning(learn from user interaction).

Ability to manually fine-tune search results.



Amazon Personalize:

FM ML service to build apps with real time personalized recommendations.

Integrates into existing websites, apps.

Used by Amazon.com to recommend.



Amazon Textract:

Automatically extracts text, handwriting, data from any scanned docs.

Extracts data from forms and tables.





##### **Amazon CloudWatch Metrics**

It provides metrics for every services in AWS.

Metric is a variablr to monitor (CPUUtilization, Networking)

Have timestamps.

CW Billing metric (us-east-1)

imp metrics:

EC2 instances: cpu uti, status check, nw

EBS volumes: disk read/writes

S3 buck: BucketSizeBytes, NumberOfObjects, AllRequests

Billing: Total estimated charge(us-east-1)

Servoce limits



CloudWatch Alarms:

Trigger notifications for any metric.

Actions:

Auto scaling, EC2 actions, SNS notifications, billing alarm.

Alarm states - OK, Insufficient\_Data, Alarm.

Handson - vd 158



CloudWatch Log:

Collect logs from - EBS, ECS, Lambda

Realtime monitoring of logs.

By def, no logs from your EC2 instance will go to CloudWatch, we need to run a CW agent on EC2 to push the log files we want with correct IAM permissions.

Prac - vd 160



Amazon EventBridge (Formerly CW events):

Schedule Cron jobs.

Schema registry.

Can archive events.

Ability to replay archived events.

Prac - 162



AWS CloudTrail:

Provides governance, compliance and audit for your AWS Account.

Enabled by def.

Get history of events/API calls made within your acc by console, sdk, cli, AWS services.

Can put logs from CT into CW logs or S3(incase of long term retention)   .

A trail can be applied to all regions(def) or a single region.

If a resource is deleted in AWS, investigate CT first.

Anytime there is an API call that needs to be looked up, CT is the ans.

Prac - 164



AWS X-Ray:

Debugging in production.

Visual analysis of our appliocations.

Troubleshooting performances(bottlenecking).

Understand dependencies in a microservice architecture.

Pinpoint service issues.

Review request behaviour.

Find errors and exceptions.

Are we meeting Service Level Agreement(SLA)?

Where is it throttled?

Identify users that are impacted.



Amazon CodeGuru:

ML powered service for automated code reviews and app performance recommendations.

2 functionalities:

CodeGuru Reviewer - automated code review for static code analysis(development), it looks at our commits.

CodeGuru Profiler - recommendations about app performance during runtime(production).

Supports Java and Python.



AWS Health Dashboard:

Service History:

Shows hostorical info for each day.

Previously called AWS Service Health Dashboard.



Overally global.

Prac - 168





##### **VPC**

IP Addresses:

IPv$ - 4.3billion addresses.

Public IPv4 can be used on internet

EC2 inst gets a new pub ip every time we restart.

Pvt IPv4 can be used on pvt nws (LAN) such as internal AWS nw - 192.168.1.0 .

Pvt ip is fixed for EC2 inst even if we restart.



Elastic ip allows us to attach fixed public IPv4 addresses to EC2 inst.

All pub ipv4 is chargeable.

IPv6 - 3.4 x 10^38 addresses.

Every ipv6 is public in AWS, it is free in AWS.

No pvt ipv6.



VPC is a virtual public cloud - private nw to deploy (regional resource).

Subnets allow us to partition our nw inside our VPC (AZ resource).

Public subnet is accessible from internet.

Pvt subnet is not accessible from internet.

Route Tables are used to define access to the internet and between subnets.

EC2, LB in public subnet.

Databases in pvt subnet as they dont need access.

IGW helps our VPCs instances to connect with the internet, public subnets have a route to the IGW.

NAT GW(AWS-managed) and NAT instances allow our instances in our Pvt Subnet to access the internet while remaining private.

Prac - 173



Network ACL:

Firewall which controls traffic from and to subnet (subnet level).

Can have allow and deny rules.

Rules only include IP addresses.

Stateless.

Security Groups:

Firewall that controls traffic to and from EC2 instance.

Can have only allow rules.

Rules include IP addresses and other security groups.

Stateful.

prac - vd 174



VPC Flow Logs:

Captures info about IP traffic going into your interfaces-

VPC flow logs, Subnet Flow logs, Elastic Network flow logs.

Helps to monitor and troubleshoot connectivity issues -

Subnets to internet, sub-sub, int-sub.

Captures nw info frm AWS managed interfaces too: ELB, Elastic Cache, RDS, Aurora.

VPC flow logs data can go to S3, CloudWatch Logs and Amazon Data Firehose.



VPC Peering:

Connect two VPC, privately using AWS' network.

Make them behave as if they were in the same nw.

Must not have overlapping CIDR(IP address range).

VPC Peering connection is not transitive(must be established for each VPC that need to communicate with one another.

VPC Flowlog - Hands-on - vd 175.

VPC Peering - same vdo



VPC Endpoints:

All the AWS services to which we r connecting, we r doing it publicly.

Endpoints allow us to connect to AWS services using a pvt nw instead of a public www nw.

This gives us enhanced security and lower latency to access AWS services.

VPC endpoint gateway : S3 and DynamoDB.

VPC Endpoint Interface: most services including S3 and DDB.

Prac - 176



AWS PrivateLink(VPC Endpoint Services):

Most secure and scalable way to expose a service to 1000s of VPCs.

Does not require VPC peering, IGW, NAT, Route Tables.

Requires a nw load balancer(Service VPC) and ENI(Customer VPC).



Site to Site VPN and Direct Connect:

-Site to Site VPN:

Connect an on-prem VPN to AWS.

The connection is automatically encrypted.

Goes over the public internet.(imp)

Fast establishment.

On-premises: must use a Customer Gateway(CGW).

AWS: must use a Virtual Private Gateway(VGW).

-Direct Connect(DX):

Establish a physical connection bet on-prem and AWS.

Connection is pvt, secure and fast.

Goes over a pvt nw. (imp).

Takes at least a month to establish.



Client VPN:

Connect from your computer using OpenVPN to your private nw in AWS and on-prem.

Allow you to connect to your EC2 instances over a private IP(just as if you were in the pvt VPC nw).

Goes over pub internet.



Transit Gateway:

Nw topologies can become complicated, to solve this, we have transit gw.

For having transitive ***peering between thousands of VPC and on-prem***, hub and spoke(star) connection.

Works with DX Gateway and VPN connections.



AWS Shared Responsibility Model:

AWS - Security of the cloud, infra, hw, sw, facilities and nw.

Customer - Security in the cloud, management of guest OS, firewall, nw config, IAM, encryption of app data.

Shared controls - patch management, config management, awareness and training.

EG:

For RDS:

AWS manages underlying EC2 instances, disable SSH access.

Automated OS, DB patching.

Audit the underlying instance and disks and guarantee it functions.

User manages ports, IP, sec group inbound rules.

Creating a db with or without pub access.

DB encryption setting.

For S3:

AWS manages - we get unlimited storage, we get encryption, ensures separation of the data between diff customers, ensures zero-day knowledge.

We manage - bucket config, bucket policy, public setting, IAM user and roles, enabling enc.



##### DDOS:

Attacker manages diff master nodes which generate a lot of bots.

DDOS protection on AWS:

AWS Shield std : no costs, provides protection from attacks such as SYN/UDP floods, Reflection attacks and other layer3/4 attacks.

AWS Shield Advanced: 24/7 premium DDoS protection, 3000 dollar per month, protects against sophisticated attacks, we will get access to response team.

AWS WAF(web app firewall): Filter specific requests based on rules, protects our web apps from common web exploits(layer 7).

Deploy an app load balan, API GW, CloudFront.

Define Web ACL, protects from SQL injection and cross-site scripting(XSS).

Rate based rules(to count occurences of events) for ddos protection.

CloudFront and Route 53: Availability protection using global edge network.

Combined with AWS Shield, provides attack mitigation at the edge.



AWS Network Firewall:

Protects our entire Amazon VPC.

From Layer 3 to Layer 7 protection.

We can inspect VPC to VPC traffic, outbound to internet, inbound from internet, to/from direct connect and site to site VPN.

Network SCL operates at subject level.

Network Firewall operates at VPC level.



AWS Firewall Manager:

Manages all sec rules in all accounts of an AWS Organisation.

Security policy: comon set of sec rules.

VPC sec groups for EC2, ALB, etc.

WAF rulea

***Manages multiple VPC sec groups across multiple accounts in an org(imp).***

Rules are applied to new resources as they are created across all and future accounts in your organisation.



Penetration testing:

AWS customers can carry out security assessments or penetration tests against their AWS infra without prior approval for 8 services - ec2, nat gw, elb, rds, floudfront, aurora, api gateways, lambda, lambda edge functions, lightsail resources, elastic beanstalk env.

Cannot do DNS zone via Amazon Route 53 hosted zones, port flooding, protocol flooding, request flooding, DDOS.



Data at rest vs Data in transit:

AWS KMS (Key management Service):

AWS manages the sw for encryption

AWS manages the enc keys for us.

Encryption opt-in:

EBS volumes, S3 buckets, Redshift db, rds db, efs drives

Encryption auto enabled: Cloudtrail logs, S3 glacier, Storage gw.



AWS CloudHSM (custom keystore):

Hardware encryption.

AWS provisions encryption hardware.

We manage our own encryption keys entirely.

Created in our HSM hardware device.

Cryptographic operations are performed within the CloudHSM cluster.



Types of KMS Keys:

Customer managed keys, 2 types - symmetric and asymmetric.

AWS managed keys - start with aws/

AWS Owned keys - AWS owns, we cannot view these.

CloudHSM Keys.

Prac - vd 188.



AWS Certificate Manager:

Used to provision, manage and deploy SSL/TLS certificates.

Provides in-flight encryption for websites(https).

Supports both pub and pvt TLS certificates.

Free of charge for public TLS certificates.

Auto TLS certificate renewal.

Integrations with ELB, CF Distribution, APIs on API Gateway.

***Service which helps us to do in-flight encryption and generates these certificates.(exam)***



AWS Secrets Manager:

Stores secrets.

Capability to force rotation of secrets every X days.

Automate generation of secrets on rotation(uses lambda).

Integration with RDS.

Secrets are encrypted using KMS.

Mostly meant for RDS integration.

Prac - 190



---

AWS Artifacts:

Not a service.

Portals that provides customers with on demand access to AWS compliance docs and AWS agreements.

Artifact Reports and Artifact Agreements.

Can be used to support internal audit or compliance.



AWS GuardDuty:

Intelligent threat discovery to protect your AWS acc.

Uses ML algorithms, anomaly detection, 3rd party data.

One click to enable, no sw needed.

Contains vpc flowlogs, cloudtrail logs, DNS logs.

Can protect against Cryptocurrency.

GuardDuty -> EventBridge -> SNS/Lambda.



Amazon Inspector:

Automated Security Assessments.

Reporting and integration with AWS Security Hub.

Send findings to Amazon Event Bridge.

It is only for EC2 instances, container images and lambda func.

Continuous scanning of the infra, only when needed.

A risk score is associated with all vulnerabilities for prioritization.



AWS Config:

Helps with auditing and recording compliance of  our AWS resources.

Helps record configurations and changes over time.

Possibility of storing the conf data into S3(analyzed by Athena).

Questions that can be solved by AWS config:

is there unrestricted ssh access to my sec group.

do the buckets have public access.

how many ALB config changed over time.

Prac - vd 194.



Amazon Macie:

Fully managed data security and data privacy service that uses ML and pattern matching to discover and protect your sensitive data in AWS.

It helps identify and alert you to sensitive data such as PII.



AWS Security Hub

Central Security tool to manage security across several AWS acc and automate security checks.

Must first enable the AWS config service.



Amazon Detective:

GuardDuty, Macie and Security Hub are used to oidentify potential security issues or findings.

It analyses, investigates and quickly identifies the root cause of security issues or suspicious activities(using ML and graphs).

Automatic collects and processes events from VPC flowlogs, cloudtrail, guardduty, create a unified view.



AWS Abuse:

Report suspected AWS resources used for abusive or illegal purposes.

Examples of abusive and prohibited behaviours:

Spam, Port scaning, Ddos, intrusion, hosting objectionable or copyright content, distributed malware.



Root user privilege:

Account owner.

Has complete access to all AWS services.

Change acc settings.
Close the AWS acc.

Change or cancel the AWS support plan.

Register as a seller in the reserved instance marketplace.



IAM Access Analyzer:

Find out which resources are shared externally:

S3 buckets, IAM roles, KMS keys, Lambda functions and layers, SQS queues, Secrets Manager Secrets.

Define ZoneofTrust = AWS acc or AWS org.

Access outside zone of trusts -> findings.

Prac - vd 200

Section 16 quiz.





Amazon Workspaces:

Managed Desktop as a service(DaaS) solution to easily provision Windows or Linux Desktops.

Great to eliminate management of on-prem VDI(Virtual Desktop Infra).

Fast and quickly scalable to thousands of users.

Pay as you goo with monthly or hourly rates.

Secured data - integrates with KMS.

Deploy workspaces as close as possible to regions.

On-demand or always on.



Amazon AppStream 2.0:

Desktop app streaming service.

Deliver to any computer, without acquiring, provisioning infra.

The application is delivered from within a web browser.

Works with any device that has a web browser.

Allows us to config an instance type per application type.



AWS IoT core:

NW of inter-connected devices that are able to collect and transfer data.

AWS IoT Core allows us to easily connect IoT devices to the AWS Cloud.

Serverless, secure and scalable to billions of devices and trillions of messages.

Apps can communicate with each other even when they are not connected.

Integrates with a lot of AWS services( lambda, S3, SageMaker,etc.).



AWS AppSync:

Store and syncdata across mobile and web apps in real time.

Used to build backend for our mobile and web apps.

Makes use of GraphQL(Mobile techno from facebook).

Client code can be generated automatically.

Integrations with DynamoDB/Lambda.

Real time subscriptions.

Offline data sync.(replaces cognito sync)

AWS Amplify can leverage AWS AppSync in the bg.

Fine grained security.



AWS Amplify:

Set of tools and services that helps you develop and deploy scalable full stack web and mobile apps.

Authentication, storage, API(REST,GraphQL), CI/CD, PubSub, Analytics, AI/ML predictions. monitoring.



AWS Infrastructure Composer:

Visually design and build serverless applications quickly on AWS.

Deploy AWS infra code without needing to be an expert in AWS.

Configure how your resources interact with each other

Generates IaC using CloudFormation.

Ability to import existing CloudFormation/SAM templates to visualize them.



AWS Device Farm:

Fully managed service that tests your web and mobile apps against desktop browsers, real mobile devices and tablets.

Run tests concurrently on multiple devices.

Ability to configure device settings.



AWS Backup:

FMS to centrally manage and automate backups across AWS services.

On-demand and scheduled backups.

Supports PITR(Point in time recovery).

Retention periods, lifecycle management, backup policies.

Cross region backup.

Cross account backup(using AWS organization.

Gets backed up to S3.



Disaster Recovery Strategies:

Backup and restore:

Cheapest - exam qs.

Pilot Light:

Warm Standby:

Higher cost

Multi-Site/Hot-Site:





AWS Elastic Disaster Recovery(DRS):

Used to be named "CloudEndure Disaster Recovery.

Quickly and easily recover your physical, virtual and cloud-based services into AWS.

Cont block-level replication for your servers.



AWS DataSync:

Move large amount of data from on-prem to AWS.

Can synchronize to Amazon S3, EFS, FSx for windows.

Replication tasks can be scheduled.

Replication tasks are INCREMENTAL after the first full load.



Cloud Migration Strategies - 7Rs - read blog

Retire - turn off things you don't need.

Retain - Do nothing for now.

Relocate - move apps from on-prem to its Cloud version.

Rehost "lift and shift" - simple migrations by re-hosting on AWS.

Replatform "lift and shift" - Migrate your database to RDS.

Repurchase "drop and shop" - Moving to different product while moving to the cloud.

Refactor/Re-architect - Reimagining how the app is architected using Cloud Native features, move from monolithic to micro-services.



AWS Application Discovery Service:

Plan migration projects by gathering info about in-prem data centers.

Agentless discovery:

Agent-based Discovery:



AWS Application Migration Service(MGN):

Lift and Shift.

Converts your physical, virtual, and cloud-based servers to run natively on AWS.

Minimal downtime, reduced cost.



AWS Migration Evaluator:

Helps us to build a data-driven business case for migration to AWS.

Provides a clear baseline of what your Organisation is running today.



AWS Migration Hub:

Central location to collect servers and applcations inventory data for the assessment, planning and tracking of migrations to AWS.

Helps accelerate your migrations to AWS.

AWS migration hub orchestrator: google

Exam qs - central location to discover access, plan and track our migration and modernization - AWS migration hub.





AWS Fault Injection Simulator(FIS):

FMS for running fault injection experiments on AWS workloads.

Stressing an application by creating disruptive events and observing how the system response.

Helps us uncover hidden bugs and performances bottlenecks.

Supports ec2, ecs, eks, rds.



AWS Step Functions:

Build Serverless visual workflow to orchestrate your lambda functions.

Features: sequence, parallel, conditions, timeouts, error handling.

Integrates with EC2, ECS, on-prem servers, API GW, SQL Queues, etc.

Possibility of implementing human approval feature.

Use cases: order fulfillment, data processing, web apps, any workflow



AWS Ground Station:

FMS which lets us control satellite communications, process data and scale our satellite operations.

Provides a global nw of satellite grounds stations near AWS regions.

Send satellite data to S3 or EC2 instance.

Use cases: weather forecasting, surface imaging, comm, video broadcasts.



AWS Pinpoint:

Scalable 2-way(outbound/inb) marketing communications service.

Supports email, SMS, voice, in-app messages.

Scales to billions of messages per day.

Use cases: run campaigns by sending marketing, bulk, transactional SMS messages.



##### **Account Management, Billing and Support.**

AWS Organizations:

Global service.

Allows us to manage multiple AWS accounts.

The main account is the master account.

Cost Benefits:

**Consolidated billing** across all accounts - single payment method.

**Pooling of reserved ec2 instances** for optimal savings.

API is available to **automate AWS account creation.**

**Restrict account privileges using Service Control Policies(SCP)**.



Multi Account Strategies:

Create acc per department, per cost center, per dev/test/prod based on regulatory restrictions (using SCP), for better resource isolation(VPC is an example)

Multi account vs One Account Multi VPC.

Organizational Unit examples:

Business Unit, Environmental Lifecycle, Project Based.

Root OU contains everything (Other OUs).



Service Control Policies:

Whitelist or blacklist IAM actions.

Applied at the OU or Account level.

Does not apply to the master acc.

SCP is applied to all the Users and Roles of the account, including root.

SCP must have an explicit allow.(does not allow anything by def).

Use cases:

Restrict access to certain services.

JSON files are present as SCP examples to either blacklist or whitelist strategies

Hands on - vd 214(skipped).



Combined Usage - combine the usage across all AWS accounts in the AWS organisations to share the volume pricing, reserved inst, and Savings Plans discounts.(exam)



AWS Control Tower:

Easy way to set up and govern a secure and compliant multi-account AWS env based on best prac.

Automates the set up of your env in a few clicks.

Automate ongoing policy management using guardrails.

Detect policy violations and remediate them.

Monitor compliance through an interactive dashboard.

AWS CT runs on top of AWS Organizations.

It automatically sets up AWS org to organize accounts and implement SCPs.

Hands on - 217.

 

AWS Resource Access Manager(ARM):

Share AWS resources that you own with other AWS accounts.

Share with any account or within your Organizations.

Avoid resource duplications.

 

AWS Service Catalog:

Users that are new to AWS have too many options, and may create stacks that are not compliant/in line with the rest of the org.

Google for more.



Pricing Models in AWS:

4 models:

Pay as you go.

Save when you reserve. - EC2 reserved instances, DynamoDB reserved capacity, etc.

Pay less by using more. - volume based discounts.

Pay less as AWS grows.



Savings Plan:

Commit to usage of individual instance families in a region.

Compute savings plan.

Machine learning savings plan.

Setup AWS cost explorer.

EC2 savings plan.



AWS Compute Optimizer:

Reduce costs and improve performance by recommending optimal AWS resources.

Lower costs by 25%.



Billing and Costing Tools:

Estimating costs in the cloud - Pricing calculator.

Tracking costs in the cloud - billing dashboard, cost allocation tags, cost explorer, cost and usage reports.

Monitoring against costs plans - billing alarms, budgets.



AWS Pricing Calculator:



AWS Billing Dashboard:



Tagging and Resource Groups:

Tags are used for organizing resources.

Tags can be used to create Resource Groups.

Cost and usage reports - it contains the most comprehensive set of AWS cost and usage data available.

Can be integrated with Athena, Redshift or QuickSight.



Cost Explorer:

Visualise, understand and manage your AWS costs and usage over time.

Create custom reports that analyse cost and usage data.

Analyze your data at high level.
Choose an optimal savings plan.

Forecast usage up to 12 months based on previous usage.



Billing Alarms in CloudWatch:

Billing data metric is stored in CloudWatch us-east-1.

Billing data are for overall worldwide AWS costs.

It's for actual cost, not for projected costs.

Not as powerful as AWS Budgets.



AWS Budgets:

Create budget and send alarms when costs exceeds the budget.

4 types of budgets - usage, cost, reservation and savings plan.

Upto 5 SNS notifications per budget.



AWS Cost Anomaly Detection:

Continuous monitor your cost and usage using ML to detect unusual spends.

Monitor AWS services, member accounts, cost allocation tags, cost categories.

Sends the anomaly detection report with root-cause analysis.



AWS Service Quotas:

Notify when u r close to a service quota value threshold.

Create CloudWatch alarms on the Service quotas console.

Eg: Lambda concurrent executions.



Trusted Advisor:

No need to install anything.

High level AWS acc assessment.

Analyze our AWS acc and provides recommendation on 6 categories:

Cost optimization, performance, security, fault tolerance, service limits, operational excellence.

Business and enterprise support plan:

Full set of checks.

Programmatic access using AWS support API.



AWS basic support plan:

Customer service and communities - 24x7 access to customer service.





#### **Advanced Identity:**

AWS Security Token Service (STS):

Enables you to **create temporary limited-privileges credentials** to access your AWS Resources.

Short term credentials, you configure expiration period.

Identify federation, IAM roles for cross/same account access.

IAM roles for amazon EC2.



Amazon Cognito:

Identify your web and mobile apps users.

Instead of creating them an IAM user, you create a user in Cognito.



Microsoft Active Directory:

Found on any windows server with AD Domain Services.

Database of objects: user accounts, computers, file shares, sec grps.

Centralized security management, create acc, assign permissions.



AWS Directory Services:

AWS managed Microsoft AD:

Create your own AD in AWS, manage users locally, supports MFA.

AD Connector:

Directory Gateway(proxy) to redirect to on-prem AD, supports MFA.

Simple AD:

AD-compatible managed directory on AWS.

Cannot be joined with on-prem AD.



AWS IAM Identity Center(Successor to AWS Single Sign-On):

One login for all your AWS acc in AWS org, business cloud apps, EC2 windows instances.

Identity providers:

Built-in identity store in IAM Identity Center.

3rd party: AD, OneLogin, Okta.



##### **AWS Architecting and Ecosystem**

Automate to make architectural experimentation easier.

Allow for evolutionary architectures.

Drive architectures using data.

Improve through game days.



Design Principles:

Scalability: Hori and Ver.

Disposable resources.

Automation - serverless, IaaS, Auto Scaling.

Loose coupling.

Services, not servers.



Well architected framework:

6 pillars:

Operational Excellence.

Security.

Reliability.

Performance Efficiency.

Cost Optimization.

Sustainability.

They are not something to balance, or trade-offs, they are synergy.



Operational Excellence:

Ability to run and monitor systems to deliver business value.

Design principles - operations as code, make frequent or small changes, anticipate failure, use managed services, learn from operational failure.

Services - AWS CF, Config, CloudTrail, CloudWatch, X-Ray, CodeBuild, Commit, Deploy, Pipeline.



Security:

Ability to protect info, systems and assets while delivering business value through risk assessments and mitigation strategies.

Design Principles - Implement string identity foundation, Enable traceability, Apply security at all layers, Automate security best prac, keep people away from data.

Services - IAM, AWS-STS, MFA token, AWS org(IAM), Config, CT, CW(Detective Controls), CF, VPC, Shield, WAF, Inspector(Infra protection), KMS, S3, ELB, EBS, RDS(data protection), IAM, CF, CW Events(incident response)



Reliability:

Ability of a system to recover from infra or service disruptions, dynamically acquire computing resources to meet demand.

DP - Test recovery procedures, auto recover from failure, scale horizintally to inc aggregate system av, stop guessing capacity, manage change in automation.

Services - IAM, VPC, Service Limits, Trusted Advisor(Foundations), Auto Scaling, CW, CT, Config(Change management), Backups, CF, S3, S3 Glacier, Route 53(Failure Management).



Performance Efficiency:

Ability to use computing resources efficiently to meet system requirements.

DP - Democratize advanced tech, go global in min, use serverless archi, Experiment more often, Mechanical sympathy.

Services - Auto Scaling, Lambda, EBS, S3, RDS(Selection), CF(Review), CW, Lambda(Monitoring), RDS, ElasticCache, Snowball, CF(Tradeoffs).



Cost Optimization:

Includes ability to run systems to deliver business value at the lowest price point.

DP - Adopt a consumption mode, measure overall efficiency, analyze and attribute expenditure, use managed and application level services to reduce cost of ownership.

Services - Budgets, Cost and usage report, cost explorer, instance reporting(Expenditure Awareness), Spot instance, reserved instance, S3 glacier(Cost-Effective Resources), Auto Scaling, Lambda(Matching supply and demand), Trusted Advisor, Cost and Usage Report(Optimizing over time).



Sustainability:

Minimises the environmental impacts of running cloud workloads.

DP - Understand your impact, establish sustainability goals, maximize utilisation, anticipate and adopt new, more efficient hardware and software offerings, use managed services, reduce the downstream impact of your cloud workloads.

Services - Auto-sca, lambda, fargate, cost explo, Spot instances, EFS-IA, S3 glacier, EBS cloud hdd, EC2(Graviton, T), S3 intelligent tiering, data lifecycle manager, RDS, Aurora, DynamoDB, CF.



AWS Well-Architected Tool:

Free tool to review your architectures against the 6 pillars Well-Architected Framework and adopt architectural best practices.

Select ur workload and answer qs and review those and against the 6 pillars.

Hands-on - vd 265



AWS Customer Carbon Footprint Tool:

Track, measure, review and forecast the Carbon Emissions generated from your AWS usage.

Helps you meet your own sustainability goals.



AWS Cloud Adoption Framework (AWS CAF):

Helps you build and then execute a comprehensive plan for your digital transformation through innovative use of AWS.

Created by AWS professionals.



AWS Right Sizing:

Choosing the most powerful instance type is not the best choice, bcz the cloud is elastic.

Scaling up is easy, so start small.

Target lowest possible cost.

Important to right size before a Cloud Migration.



AWS Ecosystem:

Blog



AWS Marketplace:

Digital catalog with thousands of software listings from independent software vendors.

Eg: custom vendors, CF templates, SaaS, Containers.
Buying from here will go to AWS bill.

Can sell our own solutions to AWS Marketplace.



AWS Training:

Google, can skip



AWS Professional Services and partner network:

AWS PS org is a global team of experts.

They work along our team and a chosen member of APN.

AWS technology partners, APN consulting Partners, APN training partners, AWS Competency program, AWS Navigate Program.



AWS IQ:

Quickly and professional help for your AWS projects.

Video conf, contract management, secure collab, integrated billing.



AWS re:Post



AWS re:Post - Knowledge Center:

Contains the most frequent and common questions and requests.



AWS Managed Services(AMS):

Provides infra and apps support on AWS.

AMS provides a team of AWS experts who manage and operate our infra for sec.



##### **Databases and Analytics:**

Storing data on disk(EFS, EBS, EC2 instance store, S3) can have its limits.

Data can be stored in a structured manner in database.

We build indexes to efficiently query/search through the data.

Can define reln bet ur datasets.

DB are optimized for a purpose and come with different features, shapes and constraints. 



Amazon RDS:

RDS - Relational DB Service.

Managed Db service for DB.

Use SQL as a query language.

Helps us to create db in cloud that are managed by AWS.:

Postgres, MySQL, MariaDB, Oracle, Microsoft SQL Server, IBM DB2, Aurora(AWS proprietary db).



Advantages over using RDS versus deploying DB on EC2:

RDS is a managed service.

Automated provisioning, OS patching.

Cont backup and restore to specific timestamp(Point in time restore).

Monitoring dashboards.

Read replicas for improved read performance.

Multi AZ setup for Disaster Recovery(DR).

Scaling capability(H and V).

Storage backed by EBS.

But we can't SSH into our instances.

RDS Solution Architecture:

ELB -> EC2 instances(possibly in an ASG) -> SQL(RD).



Amazon Aurora:

Proprietary technology from AWS(not open sourced).

PostgreSQL and MySQL are both supported as Aurora DB.

Aurora is "AWS cloud optimized" and claims 5x performance improvement over MySQL on RDS.

Auto grows in increments of 10GB, up to 256 TB.

20% more cost than Aurora but it is more efficient.



Amazon Aurora Serverless:

Automated db instantiation and auto-scaling based on actual usage.

Postgre and MySQL are both supported on Aurora Serverless DB.

No capacity planning needed.

Least management overhead.

Pay per second, can be more cost efficient.

Good for infrequent, intermittent or unpredict workloads.

Hands-on - vd 95



RDS Deployments: Read Replicas, Multi-AZ:

Read rep scales the read workload of our DB.

Can create up to 15 Read rep.

Data is only written in the main DB.



Multi-AZ:

Failover in case of AZ outage(high av).

Data is only read/written to the main db.

Can only have 1 other AZ as failover.



Multi-Region:

Disaster Recovery in case of region issue.

Local performance for global reads.

Replication cost.



Amazon ElasticCache:

It is to get managed Redis or Memcached.

Caches are in-memory db with high-performance, low latency.
Reduce load off db for read intensive workloads.

AWS takes care of OS maintenance/patching, optimizations, setup, config, monitoring, failure recovery and backups.

ElasticCache Solution Architecture - Cache :

ELB -> EC2 inst -> read/write from cache -> ElastiCache in-mem db(fast) or read/write from db -> SQL(slower).



DynamoDB:

FM High Av with replication across 3 AZ.

NoSQL db - not a relational db.

Distributed serverless db.

Scales to massive workloads.

aFast and consistent.

Single-digit millisecond latency - low latency retrieval.

Integrated with IAM for sec, authorization and administration.

Standard and Infrequent Access(IA) Table Class.



DynamoDB - type of data:

It is a key/value database.



DynamoDB Accelerator - DAX:

FM in-memory cache for DynamoDB.

10x performance improvement.

Secure, highly scalable, high av.

Difference bet ElastiCache at CCP level: DAX is only used for and is integrated with DynamoDB, while ElastiCache can be used for other db.

Hands-on - vd 99.



Redshift:

Based on PostgreSQL, but it is not used for OLTP.

It's OLAP - online analytical processing(analytics and data warehousing).

Load data once every hour, not every second.

10x better performance than other data warehouses, scale to PBs of data.

Columnar storage of data(instead of row based).

Massively Parallel Query Execution(MPP), highly av.

Pay as you go based on the instances provisioned.

Has a SQL interface for performing the queries.

BI tools such as AWS Quicksight or Tableau integrate with it.



Redshift Serverless:

Auto provisions and scales data warehouse underlying capacity.

Run analytics workloads without managing data warehouse infra.

Pay only for what you use.

Use Cases - Reporting, dashboarding apps, real-time analysis.



Amazon EMR:

Elastic MapReduce.

Helps to create Hadoop clusters(Big Data) to analyze and process vast amount of data.

Clusters can be made of 100s of EC2 instances.

Supports Apache Spark, HBase, Presto, Flink.

EMR takes care of all the provisioning and config.

Auto-sca and integrated with spot instances.

Use cases - data processing, ML, Web indexing, big data.



Amazon Athena:

Serverless query service to perform analytics against S3 objects.

Uses std SQL language to query the files.

Supports CSV, JSON, ORC, Avro and parquet(built on Presto).

Use compressed or columnar data for cost-savings(less scan).

Use cases: BI/analytics/reporting, analyze and query VPC flow logs, ELB logs, CT, etc.

Exam - analyze data in S3 using serverless SQL, use Athena



Amazon QuickSight:

Serverless ML powered business intelligence service to create interactive dashboards.

Fast, automatically scalable, embeddable, with per-session pricing.

Use cases:

BA, Building visualization, perform ad-hoc.



DocumentDB:

Aurora is an AWS implementation of PostgreSQL/ MySQL.

DDB is the same for MongoDB(NoSQL db).

MongoDB is used to store, query and index JSON data.

Similar  deployment concepts as Aurora.

FM, high av with replication across 3 AZ.

Its storage automatically grows in increments of 10GB.



Amazon Neptune:

FM graph db.

A popular graph dataset would be a social network:

User have frnds, posts have comments, comments have likes, user share and like posts.

Highly av across 3 AZ, with upto 15 read replicas.

Build and run apps working with highly connected datasets - optimized for these complex and hard queries.

Can store up to billions of relations and query the graph with milliseconds latency.

Great for knowledge graphs(Wikipedia), fraud detection, recommendation engines, social networking.



Amazon Timestream:

FM, fast, scalable, serverless time series database.

Automatically scales up/down to adjust capacity.

stores and analyses trillions of events per day.

1000s times faster and 1/10th the cost of relational databases.

Built-in time series analytics functions(helps you identify patterns in your data in near real-time).



Amazon Managed Blockchain:

BC makes it possible to build applications where multiple parties can execute transactions without the need for a trusted, central authority.

AMBC is a Managed service to join public blockchain nw or create your own scalable pvt nw.

Compatible with the frameworks Hyperledger Fabric and Ethereum.



AWS Glue:

Managed extract, transform, and load (ETL) service.

Useful to prepare and transform data for analytics.

Fully serverless service.

Glue Data Catalog: catalog of datasets.



Database Migration Service:

Quickly and secure migrate databases to AWS, resilient, self healing.

Source database remains available during the migration.

Supports homogeneous migrations : oracle to oracle.

Supports heterogeneous migrations : Microsoft SQL Server to Aurora.

Source DB - EC2 inst running DMS - target DB.

