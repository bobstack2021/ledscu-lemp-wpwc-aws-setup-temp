<!-- 
This is a WordPress Hosting Platform built on a Linux, Nginx, MySQL & PHP ("LEMP") Stack and AWS.
Hardware Overview
Laptop: Lenovo ThinkPad Carbon X1 Gen 8
Operating System: GNU + Linux | Fedora Silverblue
Virtual Machine ("VrM") Software: Gnome Boxes
Laptop: Lenovo ThinkPad Carbon X1 Gen 8
Operating System: GNU+Linux - Fedora Silverblue (immutable desktop)
Virtualization: Ubuntu 20.04 Long Term Support (“LTS”)
Cloud Amazon Machine Image (“AMI”): Ubuntu 20.04 LTS arm64; hvm:ebs-ssd
Web Application Technology Stack: Linux, Nginx, MySQL, Php7.4-fpm (“LEMP”)

AWS Cloud Infrastructure

Virtual Private Cloud (“VPC”) Overview
Naming Conventions Overview:
Everything is abbreviated and for convenience - and temporarily - the abbreviations were determined from using abbreviations.com and allacronyms.com. If pulling new abbreviations in development, please choose the government abbreviation version first (including - and especially - NASA). If there isn't a government abbreivation, then please aim to use industry specific abbreviations (if they're available). For Medical projects, one would use the "medical" abbrevaition. Regardnig the below structure and example, the company name should be abbreviated if there are abbreviations for the words that make up the co. name that equate to three (3) or more letters in an acronym. If there are less than three (3) letters, then do not use an acronym or abbrevaition and simply write out the full company name. This is in line with government policy.
The 'v' stands for "version" and the version(s) represent the sequential order/number of machines that have been provisioned, they are relational, uniform and the number is broken up into three parts:

PART ONE (1):
v1XX = Version of the overall cloud infrastructure

PART TWO (2):
vX1X = Version of the VPC that you're attaching the AWS service to

PART THREE (3):
vXX1 = version of the resource that you're creating

NAMING CONVENTION TEMPLATE
dateOfCreation-awsResourceORservice-awsRegion-versionXXX-firstNameMiddleInitial-companyName-internalOrExternal-lifeCycleStage-userRole-cloudInfrastractureORbareMetal-operatingSystemAbbreviationOS-osName-virtualMachineType-vmProviderName-serverType-serverProviderName

Example:
0915202_VPC_use-nva-1_v111_liamb-fmvmed-inter-devp-stsadm_csaisx_os-fdra-vrm-dscu-svr-dscu

FOR THIS LIVE PRODUCTION ENVIRONMENT VPC, HERE IS THE BREAKDOWN OF WHAT'S BEING USED:

Region: US-East-1 N. Virginia

Four (4) Subnets:
Private Subnet A
Private Subnet B
Public Subnet A
Public Subnet B
Route Tables
Private Route Table
Public Route Table
Internet Gateway
NAT Gateway
Elastic IP
Network ACL
DHCP Options Set
Security Groups

Elastic Compute Cloud (“EC2) Overview

Region: US-East-1 N. Virginia
Family: t4g
Type: t4g.medium
vCPUs: 2
Memory: (GiB) 4
Instance Storage (GB:) EBS only
EBS-Optimized Available: Yes
Network Performance: Up to 5 Gigabit
IPv6 Support: Yes
Enabled Termination Protection
Enabled CloudWatch Detailed Monitoring
Will NOT* delete upon termination
Encrypted Volumes - KMS Encryption
Opened Ports: SSH - Port 22, HTTP Port 80, HTTPS Port 443

In addition to that, a full resilient and redundant cloud devops infrastructure has been provisioned by way of the following:
Amazon Machine Images (AMI)
Launch Configuration Template(s)
Target Group(s)
Elastic Load Balancer(s)
Auto-Scaling Group(s)

Throughout the projects, I made it a point to use abbreviations and mirror the policies that different governing bodies had set forth, such as the Center for Medicare & Medicare (“CMS”). This seemed to be necessary and eliminate much of the confusion and technical debt that errors based on improperly named resources regularly cause. It also allows for a quicker way to identify resources within the AWS Management Console, as strictly using Identification Numbers that are automatically assigned can become confusing and have a ripple effect throughout the entire cloud infrastructure if improperly configured.

Parts of this are already BASH scripted, for example:
WEBSITEUSER | $WEBSITEUSER

However, other parts are not yet (will be quick) and need to just add variables into
the bash script list. PLEASE NOTE: we've used the TRUNCATED DOMAIN NAME for the USERNAME.
For example, if the site was: 'example.org' then the username would be 'example' 

VARIABLES TO ADD IN BASH SCRIPT:

REDACTEDSITENAME
REDACTEDMYSQLUSERPASSWORD
REDACTEDMYSQLROOTPASS
REDACTEDDBBACKUPFLE

# AWSForWordPress Plugin
# USERNAME (BELOW THIS LINE):
AWSForWordPress
REDACTEDAWSWPACCESSKEYID
REDACTEDSECRETACCESSKEY
https://REDACTEDSITENAME.signin.aws.amazon.com/console

# WP Offload Media - DISCONTINUED! NOT USING, AND ADDED TO '.gitignore' FILE...
# BUT FOR THE RECORD, here's the format:
# Access Key ID: REDACTEDWPOLMS3ACCESSKEYID
# Secret Access Key: REDACTEDWPOLMS3PASSWORD









This repo includes some code and configuration snippets from coursework and research. 
-->
