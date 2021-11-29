---
title: 'Configure JMeter'
chapter: false
weight: 33
---

## Configure JMeter

Optionally, give the JMeter test plan a suitable name, e.g. `App Runner Service Test`.

![Configure JMeter](/images/intermediate/autoscaling/service-autoscaling-jmeter-config.png)

### Add Thread Group

Then right-click on the test name and choose Add, Threads (Users), Thread Group.

![Configure JMeter Threads](/images/intermediate/autoscaling/service-autoscaling-jmeter-thread.png)

Set the number of threads to 100, and tick the infinite checkbox for loopcount as shown in the following screeenshot. This number of threads represents the total number of users performing the test script execution. The infinite checkbox continues the execution of a single thread until we manually abort the test. 

![Configure JMeter Threads](/images/intermediate/autoscaling/service-autoscaling-jmeter-thread-config.png)

### Set up HTTP Request

Right-click on Thread Group, click on **Add**, click **Sampler**, click **HTTP Request**.
An HTTP Reqeuest will be added under Thread Group.

In the server Name or IP field, enter the Default domain shown in our App Runner service Service overview section.

![Configure HTTP Request](/images/intermediate/autoscaling/service-autoscaling-jmeter-http-request-config.png)

For later analysis of the requests, add the following two Listeners.
Right-click on HTTP Request, click **Add**, click **Listener**,  click **View Results Tree**.
Right-click on HTTP Request, click **Add**, click **Listener**, click **Summary Report**.

## Run the test

Click on the green Start button above to start the load on your App Runner service.

You are asked to save the test plan before running it. Click `Yes` and save the JMeter script in your file system.