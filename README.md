# RAID 10 IMPLEMENTATION

### Introduction
*RAID 10, also known as RAID 1+0, combines the advantages of RAID 1 (mirroring) and RAID 0 (striping). It requires at least four disks. The array mirrors the data across pairs of disks for redundancy and stripes it for performance.*

### Advantages:
  - High performance due to striping.
  - High redundancy due to mirroring.

### Disadvantages:
  - Expensive since half the total storage is used for redundancy.


## Steps and Commands for RAID 10 Implementation

### 1. Prepare the Disks
  - Ensure four disks (/dev/sdb, /dev/sdc, /dev/sdd, /dev/sde) are available, unmounted, and have no existing data.

```yml

sudo umount /dev/sdb /dev/sdc /dev/sdd /dev/sde

sudo wipefs -a /dev/sdb /dev/sdc /dev/sdd /dev/sde

```

### 2. Create the RAID 10 Array
  - Use mdadm to create the RAID 10 array.

```yml
sudo mdadm --create --verbose /dev/md0 --level=10 --raid-devices=4 /dev/sdb /dev/sdc /dev/sdd /dev/sde
```
  - Explanation:

  - /dev/md0: Name of the RAID array.
  - --level=10: Specifies RAID 10.
- --raid-devices=4: Indicates four disks in the array.

### 3. Verify RAID 10 Creation
  - Check the RAID array details to ensure successful creation.

```yml
sudo mdadm --detail /dev/md0

lsblk

```

### 4. Format the RAID Array
  - Format the RAID array with a filesystem, e.g., ext4.

```yml
sudo mkfs.ext4 /dev/md0
```

### 5. Create a Mount Point
  - Create a directory where the RAID array will be mounted.

```yml
sudo mkdir /mnt/raid10
```
### 6. Mount the RAID Array
  - Mount the RAID array to the created directory.

```yml
sudo mount /dev/md0 /mnt/raid10
```

### 7. Test the RAID Array
  - Create a test file to verify the functionality of the RAID array.

```yml
sudo touch /mnt/raid10/testfile.txt

ls /mnt/raid10

```

### 8. Check Disk Usage
  - Verify the mounted RAID array and its usage.

```yml
df -h
```

### 9. Optional: Automate Mounting
  - Add an entry to /etc/fstab for persistent mounting at boot.

```yml
sudo bash -c "echo '/dev/md0 /mnt/raid10 ext4 defaults 0 0' >> /etc/fstab"
```

## Conclusion

*RAID 10 provides a robust balance of performance and redundancy, making it ideal for critical systems requiring high data throughput and reliability. These commands set up a fully functional RAID 10 array to leverage its capabilities effectively.*






