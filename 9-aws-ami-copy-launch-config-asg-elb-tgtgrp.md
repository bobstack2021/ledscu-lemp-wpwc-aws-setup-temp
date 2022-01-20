<!-- 
AMI Copy, Launch Configuration, Auto Scaling Group, Elastic Load Balancer & Target Group Creation
URL: https://docs.google.com/document/d/1IaFxnuMcyasc8NDi7NCa-fhQRN4U5B2WuI24MLsXz2k/edit

vscodium-file-title: AWS-ami-copy_launch-config_asg_elb_tgtgrp.txt

Go to EC2 Dashboard, select the newly created instance 
Right click on the instance and under the “Image and Templates” -> Select “Create Image”
Create image name
Create image description
You DO NOT need to “Enable” reboot 
Under the “Instance Volumes, you can leave the defaults, which are usually (depending on T4G-EC2 Settings
Size: 50
DO NOT enable “delete on termination” 
The Volume should already be Encrypted 
ADD Tags
Name: [copy/paste the name of the ami-copy]
Life Cycle Stage: devp (just an example)
Role: stsadm (just an example)
On the left-hand side, SCROLL DOWN to ”Auto Scaling Group” and click “Create Auto Scaling Group”
This will navigate to the other explanatory page and just click “Create Auto Scaling Group” again
Scroll down and it’s automatically set to “Configuration template” - switch to Launch Configuration then click Create Launch Configuration
This makes the initial ASG page obsolete;
One can exit that initial page and continue with the Launch Configuration creation
Under Amazon Machine Image (“AMI”), select the one that we just created
Under “Instance Type” select t4g-ec2.large 2 cores 8 gb
Under IAM Role: stsadmn (OR any other role that’s assuming this responsibility)
EBS ✅
✅ Enable Cloud Watch Monitoring
For Tags, the boiler plate should fill:
Name: [copy/paste]
Life Cycle Stage: devp  (just an example)
Role: stsadm (just an example)
***CONFIGURE THE SECURITY GROUP AND DO NOT CREATE A NEW SECURITY GROUP*** Choose the EXISTING SECURITY GROUP to avoid trouble when Launching (will get an error from about security groups not being tied/have access to the VPC)
Ports Allowed:
SSH - 80 - Anywhere (should be pre-filled)
HTTP - TCP - 0.0.0.0/0 - Anywhere
Create New Key Pair (if one would like - shouldn’t affect security group)

*** NOTE: We’ll generally create a new Launch config for each version of the app and we can create as many as we want***

CREATE THE AUTOSCALING GROUP OFF OF THE LAUNCH CONFIGURATION THAT WE JUST CREATED AND ON THE PAGE THAT WE LAND ON IMMEDIATELY AFTER CREATING THE LAUNCH CONFIG.

✅ Select the Launch Configuration that we just created 
In the dropdown menu right above to the right, click on “Create Auto Scaling Group” 
Select the VPC that we just created
Select the SAME PUBLIC-SUBNET-1A that we used for our t4g-ec2 instance
𝤿 LEAVE LOAD BALANCER AT DEFAULT (unselected)
Keep Health Checks at default settings
DO NOT SELECT ELB (we’ll create one in another step)
✅ Enable Group Metrics within Cloudwatch
Configure Group Size & Scaling Policies
Desired: 1
Minimum: 1
Maximum: 4

*** NOTE: If we have separate microservices - we can separate those out within this “Group Size & Scaling Policies” Section ***
Also NOTE, in section “291.) NACL & Security Group” of Stephane’s course, he talks about the different ephemeral…. Need to finish this explanation

TAGS
Name: [copy/paste - per usual]
Life Cycle Stage: devp (just an example)
Role: stsadm (just an example)

CREATE THE LOAD BALANCER & TARGET GROUP
This will be our “fusing load balancer” (opposed to creating one directly from the ASG creation

Can do SSL Termination
Can do basic routing which is valuable for doing difft. Tpes of microservices behind this
This will be INTERNET FACING opposed to internal
Ours is a classic internet facing one and we’ll Listen on HTTP
Configure Security Settings - ADD ALL OF THE PUBLIC SUBNETS
Don’t really need to tag this with a single load balancer - necessarily.
For Security Settings, if we were doing SSL Termination then we’d upload the certificate there (but we didn’t do this in the tutorial)
Since our instances have a public IP - we can connect with them directly with SSH
Keep the port settings @ default  - with Port 80 the only thing open
Our “Health checks”
If we were creating both a Public group and a Private group, then the Target Group would be separated to 80 & 8080, respectively (two different groups)
THE IF WE WERE load balancing across some number of instances that are NOT in an Auto-Scaling Group, then we’d set them up as the “Registered Targets’ but we don’t do this for the demo.
AFTER we create the load balancer, then we will fuse this together with the auto-scaling group
In order to automate this process, we’ll now go to the ASG and “tell it” about the Load Balancer
ADD TARGET GROUP TO AUTO-SCALING GROUP BY EDITING and it’s for the NEW APPLICATION LOAD BALANCER (NOT TARGET - WON’T FIND IT THERE)


Create Elastic Load Balancer (ELB)
This will be INTERNET FACING
Mappings: make sure that these are mapped to the PUBLIC SUBNETS
Branch off to create a new Security Group
Branch off to create a new Target Group
Don’t attach the target to the ASG until after!!! (This is from before though)
Come back and refresh both
Select the security group that we just created
Select the target group that we just created as well (it’s listening to Port 80 on “Outbound” Traffic and none on inbound as the instances themselves handle all inbound traffic - come back to fix this but whatever one it defaults to → that’s what you have listen on Port 80 and have to change to “HTTP” and 0.0.0.0/0 without a description
DO NOT ATTACH THE ELB TO A REGISTERED TARGET - JUST CREATE IT AND IGNORE THE REQUEST TO THIS IS A REVENUE SCHEME
LAUNCH!

AFTER Creating the Load Balancer: 

Navigate to the Auto Scaling Group and scroll down to the Load Balancing section and click “EDIT”
Select the Target Group we just created;
Save and DONE!!! 


WOOHOO! 
-->
