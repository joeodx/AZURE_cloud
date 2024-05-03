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
* 

