# Two Tier deployment on Azure 

![](https://pendulum-it.com/wp-content/uploads/2020/05/Azure-logo-blue.jpg)


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

* Open your web browser and navigate to the Azure Portal.
* Enter your Azure account credentials (username and password) and click "Sign in".


## Step 3  : Navigate to resource group 

* Click on resource groups. 

* You should be presented with a page where you can click the basic tab.
*  Once there make sure to pick the correct resource group(in our case it will be tech258)
* Make sure to rename the key pair name. Its best practice it to call it the same name as how you named it in your .sh folder
* Then click upload existing public key resource. 
* Bring up gitbash and copy your public key.pem then paste it in the upload key box on Azure
* Once done click submit 

## Step 5 : Fill out correct tags 

* After you have submitted you should have been presented with a page called tags.
* Its important that you change the name option to owner and the value option to your name
  

*********************************

# Deploy your first virtual machine 

## Step 1 : Create a virtual network (VNet)

"VNet" typically refers to a Virtual Network. In the context of computing and networking, a Virtual Network (VNet) is a simulated network infrastructure that provides the same functionalities and capabilities as a physical network but is created using software rather than hardware.

1. In the left-hand menu, click on "Create a resource."
2. Search for "Virtual network" and select create.
    
![](/images/121.jpg)


3. Once created navigate to the basics tab and make sure the details are the same as the one below : 

![](/images/54.jpg)


4. Navigate to the ip address tab
  
![](/images/45.jpg)





5. Click on "Subnets" and add two subnets:

6. The first one should be called **public-subnet** and the Address range should be **10.0.2.0/24**

![alt text](/images/34.jpg)


7. The second one should be called **private-subnet** and the Address range should be **10.0.3.0/24**

![](/images/234.jpg)

8. Make sure to add your tags. Name to **Owner** and your value to your **name**


Review and create the VNet. 

## Step 2 : Create your virtual machine

1. Navigate to the Azure portal and Click on "Create a resource" and search for "Virtual machine." Select it.
Fill in the required details:

 
  
2. Your basic tab should look like this :
  
![](/images/77.jpg)

3. Your disks tab should look like this :

![](/images/455.jpg)

4. You networking tab should look like this : 
  
![](/images/76.jpg)


5. Your confgure network settings tab should look like this : 

![](/images/86.jpg)

6. It should look like this : 

![](/images/done.jpg)

Click review and create and you are finished!


## Bonus Step! Automating in with user data

We can actually automate the whole process of creating our application and database by posting our whole script in the user data section in advanced tab 

1. Should look like this : 


![](/images/888.jpg)


2. Then click review and create

To check your database is running you will have to SSH into your vm using gitbash and check its status 

REMEMBER it will take the same time to deploy so wait 3-5 minutes like if you did it manually. 

You can check your applciation is running by SSH into it on gitbash or jsut put the public ip address in the URL.


## Step 3 : Repeat step 2 to create your other VM!

* Do exactly what you did again to create the vm for your application.

## Step 4 : SSh into your VM

* We need to SSh into our both Vms before we trigger our scripts to run our application 
  

* Click the connect tab like below :

![](/images/123.jpg)


Then click into native SSh to connenct!

****************************


