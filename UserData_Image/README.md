# Automating with user data
*************************

We can actually automate the whole process of creating our application and database by posting our whole script in the user data section in advanced tab. 

Make sure you have completed up until step 2 on the two_tier_deploy file and then continue here.

Also MAKE SURE YOUR SCRIPT ACTUALLY WORKS - check manually!!!

You can paste your entire script into your user data section in the advanced tab when you are makign your VM

* It should look like this : 


![](/images/121.jpg)


* Then click review and create

To check your database is running you will have to SSH into your vm using gitbash and check its status by using the ```systemctl``` command.

REMEMBER it will take the same time to deploy so wait 3-5 minutes like if you did it manually. 

You can check your applciation is running by SSH into it on gitbash or jsut put the public ip address in the URL.

*******************************************

# Creating a user image 

We can create a Image(AWI in Azure) of our instance. 

what is a AWI? 
* An AWI is a snapshot of the state of the operating system. Basically what ever we have configured in that instance, we can save and use on another one. This speeds up time as we dont have to go through the whole set up commands. 
After clicking on the create a iamge tab you should be presented with this :
  

## Step 1 : Deploying an image

First of all set up a genralised image not a specialsied image. What is the difference? 

 A generalised image is a template that does not contain specific configurations or data related to a particular workload.
 A specialised image is a template that is pre-configured with specific configurations, applications, and data tailored for a particular workload.


1. First of all ssh into your instance on gitbash 

2. You need to run the command '''waagent -deprovision+user'''
   
**This is a command used in Azure virtual machines (VMs) to prepare the VM for image capture or to generalize the VM before creating a custom image. Here's what each part of the command**does:
  

![](/images/terminalc.jpg)



<br>

3. Once you have done this make sure to goi back to your instance overview on Azure and click capture!

![](/images/image.jpg)


4. Once you have done that Make sure your settings are like this : 
  
![](/images/replaced.jpg)


5. Once you have changed the name of your image click review and create!


## Step 2 : Create a new VM

* Set up a nerw Virtual machine like normal but instead of clicking the normal ubuntu client click on see all images : 

  ![](/images/addedmore.jpg)

* Find your virtual machine you have created and select it. After this compelte the rest of the set up as usual. 

* Then add this code to your user data as you need to start it when its deployed. 

```
#!/bin/bash

echo cd app folder
cd repo/app
echo done!

echo install npm
npm install
echo done!

echo killed back
pm2 kill
echo done

echo install pm2
pm2 start app.js app
echo done
```
* If you are connecting to a datbase you also need to configure the enviorment variable. Add this command in and change the private ip address to the one your database owns

```
echo set DB_HOST env var
export DB_HOST=mongodb://10.0.3.4:27017/posts
echo done!
```
******************************************

## Step 3 SSH in and check or use ip address

1. SSh into your instance on gitbash and see if your database or applciation is working or just simply copy the public ip adress and paste it into your url. 


![](/images/screenshot%20of%20working%20app.jpg)

2.  You can use the ```cat /var/log/cloud-init-output.log``` command when you ssh into your instanceto check if the applciation had loaded.
   

Your VM should be running like ususal but now you have a image created it should load faster!


******************************************



