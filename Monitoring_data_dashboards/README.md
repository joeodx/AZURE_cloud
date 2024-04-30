# Monitoring data and responding to traffic on Azure 

## How to set up a dashboard in azure? 

* In azure click on your instance, go to overview. There you can select the monitoring tab.

![](/images/monitor.jpg)


* you can choose what graphs you want to be displayed on your dashboard


![](/images/added1.jpg)


* Now you can edit and rearrange teh dashboard to your taste.
![](/images/added2.jpg)


* You can also configure the charts to your liking. 
![](/images/added3.jpg)

*********************************************************************

## Load testing with the package Apache 

If you want to test how many requets your application can get, you need tp laod test

* First of all SSH into your app instance on gitbash
  
Then type the following command to install Apache

```
sudo apt-get install apache2-utils
```

* Once you have done that you can load test your website wit hthe follwing commmand 👍
  ```
  ab -n 1000 -c 100 http://20.90.163.1
  ```

  the n value = the total requets and the c value = how many request you are making at one time. 

You can change this value to your liking.

Then have a look at your CPU used chart and seee the results

![](/images/texting.jpg)
***************************************************

## How to set up a alert 

To create an alert on your instance dashboard go all the way down the left side bar to alert and click on it : 

![](/images/alert.jpg)

* Press create and add the alert logic you want implmented. In this case if its an amount of CPU gets used: 

![](/images/alert2.jpg)

Now if the CPU geta above your option you should recieve a email alerting you.

![](/images/email.jpg)

**********************************