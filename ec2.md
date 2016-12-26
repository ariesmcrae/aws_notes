# EC2

## Purchasing Options
1. On-demand
2. Reserved
3. Spot

## EBS Volumes
* Hard drive for your EC2 instance.
* high availability
* can be attached to any running instance in the same AZ.
* persists independently from the life of the instance.

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

