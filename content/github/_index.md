---
title: "Amazon Fusion Workshop - Deploying from Github"
chapter: true
weight: 5
pre: '<i class="fa fa-film" aria-hidden="true"></i> '
---

## Deploying a simple website to Fusion using Github

For our first example, we are going to create a simple Node.js web server which will serve a simple webpage. The runtime we select to run our web server will be NodeJS 12. Our web server will have the following components:

* index.js - a Node.js web server
* package.json - describes the library dependencies, will be used in the build step

We will build our application to install the library dependencies our web server needs - in this case, the “express” library. In order to build our application, we are going to tell Fusion to run “npm build” - this will install the express library as specified our in package.json file.

Let’s get started by creating a new Private repository on Github - this can be done by logging into Github, and then visiting https://github.com/new:

![Title Image]:(/images/github-create-repo-1.png)

