# Increase Manifold Volume
This is only necessary when the Manifold EC2 instance is running out of space and clearing the pico-engine logs and the forever logs doesn't fix the problem. 

## Extend EBS Volume Size
1. Sign in to the aws console.
1. Navigate to services->ec2
1. Click on `Volumes` under the `Elastic Block Store` menu on the left side of the screen
1. Select the manifold ec2 instance volume (Extending the `Attachment Information` column will reveal which instance the volume pertains to)
1. Right click the volume and select `Modify Volume`
1. Set the size and click Modify

## Extend Partition
1. ssh into the Manifold Instance
1. Running the command `lsblk` will show you something like:
  ```NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
     xvda    202:0    0  20G  0 disk 
     └─xvda1 202:1    0  8G   0 part /
  ```
1. test

## Extend Filesystem
