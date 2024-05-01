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