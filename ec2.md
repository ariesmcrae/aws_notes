# EC2

## Purchasing Options
1. On-demand - fixed rate per hour. No long term commitment. Use on demand (e.g. black friday sale when traffic tripples)
2. Reserved - hourly discount. Make up front payment and commit for 1 or 3yrs. Use when you always must have running VMs, with predictable usage.
3. Spot - set a bid price. When bid price >= spot price, then you purchase that spot instance. 
   When your bid price is < spot price, your instance will be terminated within 1hr. 
   Used by science companies to run their calculations, saving 50%-90%.
   Use by apps that have flexible start/end times.
   If AWS terminates the spot instance, you get the hour it was terminated in for fre.
   If you terminate the spot instance, you pay for the hour.

## EBS Volumes
* Hard drive for your EC2 instance.
* high availability
* can be attached to any running instance in the same AZ.
* persists independently from the life of the instance.
* You cannot mount 1 EBS volume to multiple EC2 instances. Instead, use EFS.
* EFS - Elastic File System. Block level storage.
* S3 - object storage.

# EBS Volume Types
1. GP2 - General Purpose SSD. Five Nine availability (99.9999%). Up to 10,000 IOPS
2. 101 - Provisioned IOPS SSD - for I/O intensive apps. > 10,000 IOPS. Designed for I/O intensive apps.
3. Magnetic (Standard) - cheap, infrequently accessed storage.


## IOPS - Input/Output Operations per second
* IOPS - the amount of data that can be read/written from EBS per second.
* Measured in KiB
* I/O size is capped at 256 KiB for SSD
* 1,025 KiB for HDD

## Root vs Additional EBA Volumes
* Every EC2 instance must have a root volume, which may/may not be EBS
* EBS root volumes are deleted when the instance is terminated, but you can choose to have EBS volumes persisted after termination.
* During creation of an EC2 instance (or afterwards), you can add additional EBS volumes to the instance.
* Additional valumes can be attached/detached onto an instance at any time. It is not deleted (by default) when instance is terminated.
* you can swap EBS volumes between different EC2 instances.

## Snapshot
* Snapshot is a backup of the EBS volume. It is not an active EBS volume. You can't attach/detach it.
* To restore a snapshot, you need to create a new EBS volume, using the snapshot as its template.

## EC2 Instance Types
* **DIRT MCG**
* **D** - Density
* **I** - IOPS
* **R** - RAM
* **T** - T2 micro cheap general purpose
* **M** - main choise for general purpose
* **C** - Compute
* **G** - Graphics

## Access Key
* Invoking AWS CLI for the first time will ask you for the :
    1. Access Key ID
    2. Secret Access Key
* AWS CLI can be used in both your laptop or your EC2 instance.    
* If you store the ~/.aws/credentials (containing the Access Key ID / Secret Access Key) in your EC2 instance, 
  and if your EC2 instance gets compromised, hacker will be be able to interact with your AWS AMI user account from their own laptop (or their own EC2 instance) via the AWS CLI.
  Therefore, it is very insecure to use the AWS Credentials inside EC2 instance. Instead, use **Roles**.

## Alternative to Access Key using Roles
* Never store your AWS Access Credentails (i.e. ~/.aws/credentials)  in EC2 instance. Instead, create a Role.
* If you want your EC2 instance to invoke AWS S3 CLI, do the following:
    1. Create a **Role** named `EC2S3Role`.
    2. Select **Role Type** `Amazon EC2` - Allows EC2 instances to call AWS services on your behalf.
    3. Attach **Policy** `AmazonS3FullAccess`.
    4. Create EC2 instance. Attach Role to the instance during creation.
* If instance gets compromised, ~/.aws/credentials is no where to be found.


## Metadata
* How to get the public ip address of your ec2 instance:
    1. ssh into your ec2 instance
    2. curl http://169.254.169.254/latest/meta-data/public-ipv4

## ELB
* ELB is not free. Charged by the hour and per gig.
* must configure one or more listeners (a process that checks for connection requests to your ELB).
```
Listeners:
    - LoadBalancerPort: '80'
      InstancePort: '80'
      Protocol: HTTP
```
* Supported ELB protocols: HTTP, TCP, SSL
* Supported ELB Ports: 1-65535


## Services that are free (but resources they create are not free)
* CloudFormation
* Beanstalk
* Autoscaling
* Opsworks


## HTTP Error Codes
* 200 - OK
* 3XX - Redirection
* 4XX - Client error (e.g. 404 not found)
* 5XX - Server error

## AWS SDKs
* aws.amazon.com/tools
* Android, iOS
* JS, Node.js
* Java, .Net
* PHP, Python, Ruby
* Go, C++

## SDK Default Regions
* Default Region - US-EAST-1 (N.Virginia)
* If no region is specified, it defaults to US-EAST-1
* Some have default regions (java)
* some do not (Node.js)