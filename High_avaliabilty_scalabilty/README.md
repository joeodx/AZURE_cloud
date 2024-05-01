# High avalaibilty and scaliabilty using a Azure VM scale set

****************************************

By leveraging Azure VM Scale Sets, you can achieve both high availability and scalability for your applications, ensuring that they remain resilient to failures and can seamlessly handle varying levels of demand.

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

6. next cchange your virtual network to your own and make sure you have the correct ports in the network interface 

![](/images/network.jpg)

7. Configure load balancer settings like below

![](/images/addedra.jpg)

**A load balancer is a device or software application that distributes incoming network traffic or workload across multiple servers or resources. Its primary purpose is to ensure that no single server gets overwhelmed by handling too much traffic or workload, thereby optimizing resource utilization, maximizing throughput, minimizing response time, and ensuring high availability and reliability of services.**

8. Go to user data box and type in the following command 

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

9. Click review and create and you should be taken to the deployment page after at least 30 seconds 

![](/images/deploymentready.jpg)

*************************************

# Part 2 : How to create your Azure VM Scale Set 

1. Now your two isntances should be running. check the instance tab on your left hand side 

![](/images/scr.jpg)

2. Copy the public address of both of them to put in your URL to see if they are both working

 ![](/images/screenshot%20of%20working%20app.jpg)

# Part 3 : Dealing with a unhealthy instance

************************

1. Stop one of your isntances then run it again. Due to the app not being able to run the script your instance should have a health state of unhealthy like below : 

![](/images/unhealthy.jpg)

2. Go into the unhealthy instance get the ssh key from the connect page  like below. Copy that into a word document : 
```
ssh -i ~/.ssh/tech258-joeod-az-key adminuser@10.0.2.7
```

* you have a private Ip at the end of the key. You can access this from outside your network, so you need to go through the load balancer.
  
The lod balance only sends traffic to the healthy instance so ther ewill be no disruption to the end user. 

3. Now change the provate ip adress to the public ip adress on your word document  below : 

```
ssh -i ~/.ssh/tech258-joeod-az-key adminuser@http://4.158.76.75/
```
4. 
