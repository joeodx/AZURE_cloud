# Learn how to do CRUD methods (create, read, update and delete) with AWS S3
*******************

What is AWS S3?

AWS S3 stands for Amazon Simple Storage Service. It's one of the core services provided by Amazon Web Services (AWS). S3 is a scalable storage service designed to store and retrieve any amount of data from anywhere on the web.

**Key features** : 

* Its a simple storage service 
* It can store and retrieve andy type of data from anytime from anywhere, with no organisation
* It can host static website on the cloud 
* Things 
* A blob can be store in Aws BUCKET 
* The default is everything is private but you can config to make public.
* it is built from the ground up, so there is reduncy you can tweak 
* Azure there are blobs stored in three places within the same data center
* You can access it via the AWS console, AWS cli and pythoin boto3


## Steps to access AWS s3 and com-plete CRUD functions.

1. Create a brand new instance on AWS, Set it up like normal but make sure your ubuntu image has the follwoing settings 

```

Ubuntu Server 22.04 LTS

tech258-Joe-learn-s3-vm

SSH into instance
```

2. Once you have set that up make sure to ssh into your instance in gitbash. 

3. What do we do always when we ssh into our instance? **UPDATE AND UPGRADE**

```
sudo apt update -y

sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
```

3. Now we need to install python 3 and AWS. Add the following commands 👍

```
# check if pyhton 3 is already installed
python3 --version 

sudo apt-get install python3

sudo apt-get install python3-pip -y

#install aws cli
sudo pip install awscli 

# version check
aws --version 
```

4. Next you need to rename python  - use the ALias command
   
   ```
   alias python=python3 
   ```
   
   

5. 
   Add the follwing command to authenticate with specific ID and secret access ID!
   (your secret key folder should be in your ssh folder)

```
aws configure
< access key> : <your key goes here>
< secret key> : <your key goes here>
# region name: eu-west-1
# output: json
```


Now you are in and verified! 

6. Use the command to check that you can see all buckets

```
aws s3 ls
```

# Part 2 - Crud commands in Aws s3
******************
* If you want to **create a new bucket**, use the follwoing command ( I am going to use my name for the example): 
```
aws s3 mb s3://tech258-joe-first-bucket # --region eu-west-1
```

  If you get rid of the ```region eu-west-1``` command, the region will be set to the same region you used to set up your VM. 

*  If you want to **list a bucket**, use the following command : 
   
```
aws s3 ls s3://tech258-muyis-first-bucket
```
   If you want to **upload a file to a bucket**, use the following command : 
   1. First make the file : 
```
echo This is the first line in a test file > test.txt
```
2. Then copy into the file
```
aws s3 cp test.txt s3://tech258-muyis-first-bucket
```

* Downlaod fiels from the bucket 
  ```
  mkdir downloads
  ```

* sync to copy 
  ```
  aws s3 sync s3://tech258-muyis-first-bucket
  ```
* rm to remopve a file 
```
aws s3 rm s3://tech258-muyis-first-bucket/test.txt
```
## Part 3 - Delete commands 
 💥
 You have to be extra careful with these commands: 

* This will remove everything in a bucket
  
  ```
  aws s3 rm s3://tech258-muyis-first-bucket --recursive
  ```

* Remove only empty buckets 
  ```
  aws s3 rb s3://tech258-muyis-first-bucket
  ```
* Remove the buckets and its contents 
  ```
  aws s3 rb s3://tech258-muyis-first-bucket --force
  ```

***************************


# Boto3 Documentation 
*************************
## What is Boto3? 
* Boto3 is the official AWS SDK for Python. It allows developers to interact with AWS services programmatically using Python scripts. 
* Boto3 provides a high-level API that makes it easy to create, configure, and manage AWS resources, including S3 buckets and objects.

 1. Install Boto3 with the follwoing command 👍

```
pip install boto
```

Now lets crerate our scripts!

## Part one : 

1. Create a python script file in your instance on gitbash 
   ```
   lists-buckets.py
   ```
2. use the command below to list all the buckets
```
aws s3 ls
```
### List all the S3 buckets
Now you can run the script to lists all the S3 buckets below : 

```
import boto3

# Create an S3 client
s3 = boto3.client('s3')

# List all S3 buckets
response = s3.list_buckets()

# Print bucket names
print("List of S3 Buckets:")
for bucket in response['Buckets']:
print(bucket['Name'])
```
### Create an S3 Bucket 

1. Create a python script file in your instance on gitbash 
   ```
   create-buckets.py
   ```

In this 













