---
title: 'Install and Run hey'
chapter: false
weight: 32
---

## Install hey

Go to the [hey Github page](https://github.com/rakyll/hey) and follow the installation instructions for your operating system to install hey.


## Run the load

The following hey command generates HTTP requests with 200 concurrent clients and lasts for 3 minutes. Find the URL of your service in the App Runner console.

```shell
$ hey -c 200 -z 3m https://xxxxxxxxxx.region.awsapprunner.com/
```

Move on to the next section to see the changing metrics of your App Runner service.