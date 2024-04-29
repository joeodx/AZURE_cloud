# Automating in with user data

We can actually automate the whole process of creating our application and database by posting our whole script in the user data section in advanced tab. 

Make sure you have completed up until step 2 on the two_tier_deploy file and then continue here.

Also MAKE SURE YOUR SCRIPT ACTUALLY WORKS - check manually!!!

You can paste your entire script into your user data section in the advanced tab when you are makign your VM

* It should look like this : 


![](/Two_Tier_deploy/images/888.jpg)


* Then click review and create

To check your database is running you will have to SSH into your vm using gitbash and check its status by using the ```systemctl``` command.

REMEMBER it will take the same time to deploy so wait 3-5 minutes like if you did it manually. 

You can check your applciation is running by SSH into it on gitbash or jsut put the public ip address in the URL.

*******************************************

# Creating user image 

We can create a Image(AWI in Azure) of our instance. 

what is a AWI? 
* An AWI is a snapshot of the state of the operating system. Basically what ever we have configured in that instance, we can save and use on another one. This speeds up time as we dont have to go through the whole set up commands. 
After clciking on the vreate a iamge tab you should be presented with this
  
![](/Two_Tier_deploy/images/1212.jpg)


# Deploying an image




then after this create your virtual machine normally 