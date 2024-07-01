
# Backup file from EC2 to S3
This tutorial encompass all the steps to create and AWS EC2 instance, working on file than stored them each minute on a S3 backup as zip file.
Before following this tutorial, make sures you have a active AWS account and nows how launch and stop AWS services when needed.

## Step 1: Creating a EC2 Instance
Amazon EC2 (Elastic Compute Cloud) is AWS service that allows you work with virtual machine in the cloud.


## Step 4: Scripting the backup
Once your EC2 instance launched, your S3 bucket created then related, you can created your bash script:
1. Create the backup bash script
```
#!/bin/bash

# Define variables
SOURCE_FOLDER="/path/to/your/folder"
S3_BUCKET="your-s3-bucket-name"
TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")
BACKUP_FILE="/tmp/backup_$TIMESTAMP.tar.gz"

# Create a compressed backup file
tar -czf $BACKUP_FILE $SOURCE_FOLDER

# Upload the backup to S3
aws s3 cp $BACKUP_FILE s3://$S3_BUCKET/

# Remove the local backup file
rm $BACKUP_FILE
``` 
2. Make the script executable
```
chmod u+x script.sh
```
3. Schedule the Script to Run Every Minute
```
* * * * * /path/to/your/script.sh
```