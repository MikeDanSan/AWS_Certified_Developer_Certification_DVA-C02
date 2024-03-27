# Section 6: EC2 Instance Storage (vid #55 summary) (EC2 Data Management Quiz)

## Elastic Block Storage (EBS) EBS volumes

- Network connected
- MULTI EC2 CAN NOT attach to ONE EBS at a time (except multi-attach ONLY for io 1/ io 2 type)
  - Attach the same EBS volume to multiple EC2 instances in the same AZ
- Multi EBS can attach to an EC2 instance
- Locked at the Availability Zone (AZ) level.
- snapshot EBS volumes to use Global infrastructure
- gp2: IO increase if disk size increases (COUPED/ SYNCED)
- gp3 & io 1: increases IO and Disk size separately (INDEPENDENTLY)
- ROOT EBS Volumes are by DEFAULT terminated when EC2 instance is removed (Can be disabled)
- Other EBS volumes are NOT DEFAULT terminated. (Can be Enabled)
- Only EBS volume types that can be used as boot volumes: gp2, gp3, io1,io2, and Magnetic (Standard)
- EBS volume type st1 and sc1 (super cheap) can not be used for boot. (Hard Disk Drives (HDD))
- EBS gp2 volumes max IOPS 16,000 ~ 5334 GB

## Elastic File System (EFS)

- Network File System (NFS)
- Use case mount 100s of instances across AZ
- ONLY for Linux instances (POSIX)
- MUTLI EC2 instance in different AZ's attach to SINGLE EFS (using Security Groups)
- EFS is more costly then EBS but has a cost savings option for EFS-IA (Elastic File System Infrequent Access)

## Instance store

- Physically attached to EC2 instance so lose instance you lose instance store.
- Used for Performance and dont mind losing the data upon termination or can be lost. (cache)
- HIGHEST IOPS.

## Amazone Machine Image (AMI)

- Are tied to the region.
