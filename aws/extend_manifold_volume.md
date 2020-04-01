# Extend Manifold Volume
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
     xvda    202:0    0  16G  0 disk 
     └─xvda1 202:1    0  8G   0 part /
  ```
1. run the command `sudo growpart /dev/xvda 1` with xvda coming from the device name and 1 coming from the partition number output by the last command
1. Running the command `lsblk` will now show you something like:
  ```NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
     xvda    202:0    0  16G  0 disk 
     └─xvda1 202:1    0  16G   0 part /
  ```
  
## Extend Filesystem
1. Run `df -Th` to find the filesystem type. You should see something like
  ```Filesystem     Type      Size  Used Avail Use% Mounted on
     /dev/xvda1     ext4       16G  7.5G  8.1G  48% /
  ```
1. Because our filesystem type is ext4, we run the command `sudo resize2fs /dev/xvda1`
1. Finally, run `df -h` to confirm the changes took place.

