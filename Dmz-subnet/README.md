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


