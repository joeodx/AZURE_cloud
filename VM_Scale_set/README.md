# High avalaibilty and scaliabilty using a Azure VM scale set

****************************************

By leveraging Azure VM Scale Sets, you can achieve both high availability and scalability for your applications, ensuring that they remain resilient to failures and can seamlessly handle varying levels of demand.


Azure Virtual Machine Scale Sets (VMSS) is a service provided by Microsoft Azure that allows you to create and manage a group of identical virtual machines. These virtual machines are configured to handle a large workload and can automatically scale in or out based on demand.

* **High availabilty** is vital for popular, public-facing cloud services, and is a key metric for DevOps engineers. We need to ensure that services are consistently accessible and operational, minimizing downtime and service disruptions.

* **Scalability** allows our application to meet variying demand. We can scale up capacity when our application is seeing a lot of traffic, and scale down the number of virtual machines when we are seeing less demand.

![](/images/HIAV.jpg)


# How to create your Azure VM Scale Set 

***************************************

Before you get started make sure your custom image is working properly. This is important for the following steps. 

1. Search for virutal machine scale set in your search bar and then click create:
   

![](/images/screenshot%20server.jpg)
<br>
![](/images/downlaod.jpg)


2. Once you click create make sure to have the following options the same(make sure to have the same zones configured) : 

![](/images/copy.jpg)

3. Make sure to change scalling option to Autoscailing : 

![](/images/autoscailing.jpg)

4. Click on configure scaling options and have your settings identical to this : 

![](/images/configure2.jpg)

5. Make sure you change the image selecton to your image 

![](/images/imageadded.jpg)

6. next change your virtual network to your own and make sure you have the correct ports in the network interface 

![](/images/network.jpg)

7. Configure load balancer settings like below

![](/images/addedra.jpg)

**A load balancer is a device or software application that distributes incoming network traffic or workload across multiple servers or resources. Its primary purpose is to ensure that no single server gets overwhelmed by handling too much traffic or workload, thereby optimizing resource utilization, maximizing throughput, minimizing response time, and ensuring high availability and reliability of services.**


8. Make sure you have these settings for health : 

![](/images/screa.jpg)

9.  Go to user data box and type in the following command 

```
!/bin/bash

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

10. Click review and create and you should be taken to the deployment page after at least 30 seconds 

![](/images/deploymentready.jpg)

*************************************

# Part 2 : How to create your Azure VM Scale Set 

1. Now your two instances should be running. check the instance tab on your left hand side 

![](/images/scr.jpg)

2. Copy the public address of both of them to put in your URL to see if they are both working

 ![](/images/screenshot%20of%20working%20app.jpg)

# Part 3 : Dealing with a unhealthy instance

************************

1. Stop one of your instances then run it again. Due to the app not being able to run the script your instance should have a health state of unhealthy like below : 

![](/images/unhealthy.jpg)

* Remember you configured your loader settings to check every 10 minutes for updates. So this will be how long at least until you get an update on the health state.

2. Go into the unhealthy instance get the ssh key from the connect page  like below. Copy that into a word document : 
```
ssh -i ~/.ssh/tech258-joeod-az-key adminuser@10.0.2.7
```

* You have a private Ip at the end of the key. You can not access this from outside your network, so you need to go through the load balancer.
  
The load balancer only sends traffic to the healthy instance so ther ewill be no disruption to the end user. 

3. Now change the private ip adress to the public ip adress of the load balancer and then -p port 0f 50001 : 

```
ssh -i ~/.ssh/tech258-joeod-az-key -p 50001 adminuser@http://4.158.76.75/
```
4. Now SSH into your unhealthy instance with that command. You can trobleshoot what the issue is. 


# Part 4 : Deleting a VM scale Set and all its connecting parts
*******************


1. Delete the load balancer.
2. Then delete the ip address. 
3. Then the scale set.

*************************
