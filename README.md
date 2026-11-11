# WORKING WITH EBS
## NAME: SAMEER SHARIFF M
## REG NO: 212224220085

## Aim

To create and configure an Amazon Elastic Block Store (EBS) volume, attach and mount it to an Amazon EC2 instance, create a snapshot backup, and restore the snapshot to a new EBS volume.

---

## Algorithm / Steps

1. Create a new Amazon EBS volume with a size of 1 GiB.
2. Select the same Availability Zone as the EC2 instance.
3. Attach the EBS volume to the EC2 instance using `/dev/sdb`.
4. Connect to the EC2 instance using AWS Systems Manager Session Manager.
5. Check the available storage using `df -h`.
6. Create an `ext3` file system on the EBS volume.
7. Create the `/mnt/data-store` directory.
8. Mount the EBS volume to `/mnt/data-store`.
9. Configure `/etc/fstab` for automatic mounting.
10. Verify that the EBS volume is successfully mounted.
11. Create `file.txt` inside the mounted EBS volume.
12. Verify the contents of the created file.
13. Create an EBS snapshot named `My Snapshot`.
14. Delete `file.txt` from the original EBS volume.
15. Create a new EBS volume from the snapshot.
16. Attach the restored volume to the EC2 instance using `/dev/sdc`.
17. Create the `/mnt/data-store2` directory.
18. Mount the restored volume to `/mnt/data-store2`.
19. Verify that `file.txt` has been successfully restored.

---

## Program

### 1. Check Available Storage

```bash
df -h
```

### 2. Create an ext3 File System

```bash
sudo mkfs -t ext3 /dev/sdb
```

### 3. Create a Mount Directory

```bash
sudo mkdir /mnt/data-store
```

### 4. Mount the EBS Volume

```bash
sudo mount /dev/sdb /mnt/data-store
```

### 5. Configure Automatic Mounting

```bash
echo "/dev/sdb   /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
```

### 6. View the File System Configuration

```bash
cat /etc/fstab
```

### 7. Verify the Mounted Volume

```bash
df -h
```

### 8. Create a File in the EBS Volume

```bash
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
```

### 9. Read the File

```bash
cat /mnt/data-store/file.txt
```

### 10. Delete the File

```bash
sudo rm /mnt/data-store/file.txt
```

### 11. Verify File Deletion

```bash
ls /mnt/data-store/
```

### 12. Create a Mount Directory for the Restored Volume

```bash
sudo mkdir /mnt/data-store2
```

### 13. Mount the Restored EBS Volume

```bash
sudo mount /dev/sdc /mnt/data-store2
```

### 14. Verify Snapshot Restoration

```bash
ls /mnt/data-store2/
```

Expected output:

```text
file.txt
```

---

## Outputs
<img width="1917" height="1093" alt="Screenshot 2026-11-06 085405" src="https://github.com/user-attachments/assets/d62f3c77-e0ca-49dc-b8bf-e2de1d2216de" />
<img width="1906" height="1085" alt="Screenshot 2026-11-06 085431" src="https://github.com/user-attachments/assets/a0aad58a-8b43-4bb2-b4de-74b6f9052179" />
<img width="1917" height="1068" alt="Screenshot 2026-11-06 085511" src="https://github.com/user-attachments/assets/b4c40ea7-5b55-4122-90a8-665c1ef4534d" />
<img width="1917" height="1093" alt="Screenshot 2026-11-06 085605" src="https://github.com/user-attachments/assets/10b76f40-ad11-4f44-8f28-c39b4ec45e7f" />
<img width="1917" height="1092" alt="Screenshot 2026-11-06 085758" src="https://github.com/user-attachments/assets/65cb9037-c367-4759-ad7c-d66dd8cc20b1" />
<img width="1917" height="1095" alt="Screenshot 2026-11-06 085841" src="https://github.com/user-attachments/assets/3e03849d-6d3c-492e-83b4-15dcda47668a" />
<img width="1917" height="1093" alt="Screenshot 2026-11-06 090121" src="https://github.com/user-attachments/assets/c90e5bb5-6641-4973-826b-d9d4a321a753" />
<img width="1917" height="1085" alt="Screenshot 2026-11-06 090341" src="https://github.com/user-attachments/assets/5aa95b8d-dcf3-4fd6-97f6-5ccaed18a6a3" />
<img width="1917" height="1096" alt="Screenshot 2026-11-06 090416" src="https://github.com/user-attachments/assets/0d138de7-0407-45f4-ba10-b39dd50e67c5" />
<img width="1917" height="1097" alt="Screenshot 2026-11-06 090543" src="https://github.com/user-attachments/assets/269d4073-21a3-4272-8f64-bd80e4193639" />
<img width="1917" height="1095" alt="Screenshot 2026-11-06 090612" src="https://github.com/user-attachments/assets/1f4a26e6-8e0c-4c75-b1bb-9fe94c5940bb" />
<img width="1917" height="1092" alt="Screenshot 2026-11-06 090632" src="https://github.com/user-attachments/assets/201cfe0f-e299-4905-bdf4-0a235b6cac2b" />
<img width="1917" height="1092" alt="Screenshot 2026-11-06 091001" src="https://github.com/user-attachments/assets/43dc560a-0f8e-4ee1-b4bb-24003d12317d" />
<img width="1917" height="1097" alt="Screenshot 2026-11-06 091136" src="https://github.com/user-attachments/assets/e606dd4d-176f-4ce5-8075-915e93c9b61c" />
<img width="1917" height="1093" alt="Screenshot 2026-11-06 091536" src="https://github.com/user-attachments/assets/84cf1141-ee38-41bb-937a-797a40bef1d5" />
<img width="1917" height="1092" alt="Screenshot 2026-11-06 091558" src="https://github.com/user-attachments/assets/99eb22e3-c274-4097-8514-f0607b934b9c" />
<img width="1917" height="938" alt="Screenshot 2026-11-06 091659" src="https://github.com/user-attachments/assets/84b476f5-ff3d-4862-98f8-a31cc87e19c5" />
<img width="1916" height="1093" alt="Screenshot 2026-11-06 092217" src="https://github.com/user-attachments/assets/d916e619-151d-44e7-bef8-87a26b680c7e" />
<img width="1917" height="1087" alt="Screenshot 2026-11-06 092335" src="https://github.com/user-attachments/assets/45b6810f-ec2a-4238-8c9f-18f4826d166a" />
<img width="1882" height="1088" alt="Screenshot 2026-11-06 092425" src="https://github.com/user-attachments/assets/567c1a60-361c-4a75-8c59-5eae88f5cbd9" />
<img width="1917" height="937" alt="Screenshot 2026-11-06 092532" src="https://github.com/user-attachments/assets/134040f2-4bfd-4af8-9b02-0d8c72fd8bd1" />
<img width="1917" height="1100" alt="Screenshot 2026-11-06 092715" src="https://github.com/user-attachments/assets/381002e7-7858-457a-8e86-0651bf04491d" />






## Result
Thus, an Amazon EBS volume was successfully created and attached to an Amazon EC2 instance. The volume was formatted with an ext3 file system, mounted, and used for storing data. An EBS snapshot was successfully created as a backup, and a new EBS volume was restored from the snapshot. The previously deleted file.txt was successfully recovered, demonstrating the backup and restore functionality of Amazon EBS.

