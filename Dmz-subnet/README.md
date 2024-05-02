# Dmz subnet setting up
****************************



* A DMZ (Demilitarized Zone) subnet is a segmented portion of a network that acts as a buffer zone between an organization's internal network (intranet) and the external network, usually the internet. 
* The primary purpose of a DMZ subnet is to provide an additional layer of security by hosting services that need to be accessible from both the internet and the internal network, such as web servers, email servers, or FTP servers.

* Heres a diagram of a 3 subnet architecture 
  
![](/images/21.jpg)

## Steps to set up NVA Vm 

We need to know how to set up a 3 subnet architecture. This will add security and control who can access certian parts of our application.

1. Create a brand new virtual network. You can search for it in the search bar and then click create

![](/images/convert.jpg)

2. Change to the right resource group and give it a relative name then set up the rest of the basics like normal

![](/images/screensa.jpg)

3. **This is the important bit** go to network settings and make sure to add three subnets. 
   * The first will be for your deployed app VM so change the name to ```public-subnet``` and make sure the starting address is the following ```10.02.0/24```
   * The second will be for your Nva Vm. Give it the name ```DZN-subnet``` and make sure the starting address is ```10.0.3.0/24```
   * The third will be for your Database VM. Give it the name ```private subnet``` and the starting address to ```10.0.4.0``` 

![](/images/ip.jpg)


4. Make sure to add your tags, check everything is correct and click create!

5. Your New subnet should be created now. Click overview to check!

![](/images/addedd.jpg)

## Part 2 - Set up a db VM

1. Now that you have set up your subnet go to your images and click on your ```db-deply-image-db``` to create a virtual machine for your db. 

2. Set up the basic tab like normal and the disk tab.

![](/images/screen.jpg)

3. Go to Network tab  and change your ```virtual network``` to your new subnet you created earlier. In my case it was ```tech258-joeod-3-subnet-vnet```
   * Change the ```subnet``` to private subnet
   * Change the ```public``` ip to none

* We done need a public Ip because we should only ssh into our db.
 
![](/images/networkingtab2.jpg)

4. You dont need to add anything to user data for your db so just fill out the tags. then click review and create.

![](/images/takes.jpg)

## Part 3 - Set up a app VM

Now that is loading you can set up your application VM.

1.  Now that you have set up your db VM go to your images and click on your ```db-deply-image-app``` to create a virtual machine for your app. 
   
2.  Set up the basic tab like normal and the disk tab but allow HTTP ports 80.

![](/images/app.jpg)

3. Go to Network tab  and change your ```virtual network``` to your new subnet you created earlier. In my case it was ```tech258-joeod-3-subnet-vnet```
   * Change the ```subnet``` to public subnet with the ```10.0.2.0/24```
   * make sure You rename itit to public-subnet
  
![](/images/jpgd.jpg)

