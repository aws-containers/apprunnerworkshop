---
title: 'App Runner Metrics'
chapter: false
weight: 34
---

## Metrics

Open the Metrics tab of your App Runner service.
It takes a few minutes to see changes in our App Runner service.

The request count will have a peak. The number of active instances will increase as shown in the following screenshots.

![Request Count](/images/intermediate/autoscaling/service-autoscaling-request-count.png)

![Active Instances](/images/intermediate/autoscaling/service-autoscaling-active-instances.png)

Click on the three dots next to a metric field and select "Enlarge" to view the metric in a larger window, or click "View in metrics" to explore the metrics in the Cloudwatch console.

## JMeter

Additionally to the App Runner service metrics, you can also explore the JMeter summaries which we created before..

On the left side, click `View Results Tree` and explore the details of each single HTTP request by clicking on the requests. Explore also the summary of the test by opening the `Summary Report`.

Go to the next page to stop the JMeter load on your App Runner service.