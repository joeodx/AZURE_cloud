# Monitoring data and responding to traffic on Azure 
**************************

## How to set up a dashboard in azure? 

1. In azure click on your instance, go to overview. There you can select the monitoring tab.

![](/images/monitor.jpg)


2. You can choose what graphs you want to be displayed on your dashboard


![](/images/added1.jpg)


3. Now you can edit and rearrange teh dashboard to your taste.

![](/images/added2.jpg)


4. You can also configure the charts to your liking. 

![](/images/added3.jpg)

*********************************************************************

## Load testing with the package Apache 

* If you want to test how many requets your application can get, you need to do load test. 
* The main objective of a load test is to determine the system's behavior concerning its response time, throughput, and resource utilization when subjected to various levels of simulated user activity or workload.

1. First of all SSH into your app instance on gitbash
  
2.  Then type the following command to install Apache

```
sudo apt-get install apache2-utils
```

3.  Once you have done that you can load test your website wit hthe following commmand 👍
  ```
  ab -n 1000 -c 100 http://20.90.163.1
  ```

  ***The n value = the total requets and the c value = how many request you are making at one time.***

4. You can change this value to your liking.

5. Then have a look at your CPU used chart on your dashboard and seee the results!

![](/images/texting.jpg)
***************************************************

## How to set up a alert 

1. To create an alert on your instance dashboard go all the way down the left side bar to alert and click on it : 

![](/images/alert.jpg)

2. Press create and add the alert logic you want implmented. In this case if its an amount of CPU gets used. 
3. The operator is changed to greather than and the threshold value to 6.
   

![](/images/alert2.jpg)

4. Now if the CPU is greater than 6 above you should recieve a email alerting you if yur CPU goes over 6% like below. 

%. You can test the alert by using the Apache commands you learnt earlier. 

![](/images/email.jpg)

**********************************