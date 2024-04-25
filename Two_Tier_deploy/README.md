# Two Tier deployment on Azure 

*******************************************

## Step 1 : Generate the SSH key

* We need to generate the ssh key first to use with Azure. 
* So open gitbash , cd into your ssh dolder and type the follwing command 

```python
ssh-keygen -t rsa -b 4096 -C "<YOUR_EMAIL>
```

* After its generated make sure toaccess the pem file so you can see your public key. : Yo ucan do that by the follwing command 

```
cat <keyname.pem>
```

* You should be able to see your full public key...keep this ready we going to need it for AZURE.

## Step 2 : Log into Azure Portal 

* Open your web browser and navigate to the Azure Portal.![](https://azure.microsoft.com/en-gb/free/search/?ef_id=_k_2a8b609977cc14f1919206b327a52ba3_k_&OCID=AIDcmm3bvqzxp1_SEM__k_2a8b609977cc14f1919206b327a52ba3_k_&msclkid=2a8b609977cc14f1919206b327a52ba3)
* Enter your Azure account credentials (username and password) and click "Sign in".

## Step 3 : Log into Azure Portal 

* Open your web browser and navigate to the Azure Portal.![](https://azure.microsoft.com/en-gb/free/search/?ef_id=_k_2a8b609977cc14f1919206b327a52ba3_k_&OCID=AIDcmm3bvqzxp1_SEM__k_2a8b609977cc14f1919206b327a52ba3_k_&msclkid=2a8b609977cc14f1919206b327a52ba3)
* Enter your Azure account credentials (username and password) and click "Sign in".

## Step 4 : Navigate to resource group 

* Click on resource groups. 
* You should be presented with a page where you can click the basic tab.
*  Once there make sure to pick the correct resource group(in our case it will be tech258)
* Make sure to rename the key pair name. Its best practice it to call it the same name as how you named it in your .sh folder
* Then click upload existing public key resource. 
* Bring up gitbash and copy your public key.pem then paste it in the upload key box on Azure
* Once done click submit 

## Step 5 : Fill out correct tags 

* After you have submitted you should have been presaented with a page called tags.
* Its important that you change the name option to owner and the value option to your name
  

*********************************

# Deploy your first virtual machine 

## Step 1 : Create a virtual network (VNet)

* Navigate to the Azure portal (https://portal.azure.com).
* In the left-hand menu, click on "Create a resource."
* Search for "Virtual network" and select it.
* Click on "Create" to begin configuring the VNet.

![](/images/12.jpg)

* Fill in the following details:
 - Name: tech258-yourname-2-subnet-vnet
 - Address space: 10.0.0.0/16
  
* Click on "Subnets" and add two subnets:
 Subnet 1:
Name: public-subnet
Address range: 10.0.2.0/24
Subnet 2:
Name: private-subnet
Address range: 10.0.3.0/24

* This is going to be important when it comes to deploying our db and application 

Review and create the VNet. 

## Step 2 : Create your virtual machine

* Navigate to the Azure portal and Click on "Create a resource" and search for "Virtual machine." Select it.
Fill in the required details:

* Virtual machine name: Choose a name for your VM.
Region: Choose the desired region.
Image: Ubuntu Pro 18.04 LTS - x64 Gen2
Size: Standard_B1s
Authentication type: SSH public key
Username: adminuser
SSH public key: Upload your SSH public key.
Disks:
OS disk type: Standard SSD
Networking:
Virtual network: Select the VNet created earlier (tech258-yourname-2-subnet-vnet).
Subnet: Choose the public-subnet.
Public IP: Choose "None" (assuming you don't need a public IP).
Network security group: Create a new NSG and configure it to disallow MongoDB port.
Management:
Tags: Add a tag for the owner.
Review and create the VM.
