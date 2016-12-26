# EC2

## Purchasing Options
1. On-demand - fixed rate per hour. No long term commitment. Use on demand (e.g. black friday sale when traffic tripples)
2. Reserved - hourly discount. Make up front payment and commit for 1 or 3yrs. Use when you always must have running VMs, with predictable usage.
3. Spot - set a bid price. When bid price >= spot price, then you purchase that spot instance. 
   When your bid price is < spot price, your instance will be terminated within 1hr. 
   Used by science companies to run their calculations, saving 50%-90%.
   Use by apps that have flexible start/end times.
   If the spot instance is terminated by AMZ, you will not be charged for a partial hour. If you terminate the instance yourself, you will be charged for any hour.

## EBS Volumes
* Hard drive for your EC2 instance.
* high availability
* can be attached to any running instance in the same AZ.
* persists independently from the life of the instance.
* You cannot mount 1 EBS volume to multiple EC2 instances. Instead, use EFS.

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
* DIRT MCG
* D - Density
* I - IOPS
* R - RAM
* T - T2 micro cheap general purpose
* M - main choise for general purpose
* C - Compute
* G - Graphics

