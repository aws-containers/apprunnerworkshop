---
title: "Fork & clone the service repo"
chapter: false
weight: 16
---

## Fork the sample app

Go to https://github.com/andskli/repostatus-gh-demo and click fork in the upper right
corner, select *your username* to fork to. Now you have a fork of the simple demo app that we can
modify and test.

## Clone your forked repository

Change the placeholder in the comand below to match your GitHub username.

```bash
cd ~/environment
git clone https://github.com/[MY_GITHUB_USERNAME]/repostatus-gh-demo.git
```

## What's in the repo?

The demo app is a very simple Python web app that fetches data from the GitHub API and caches the
data in DynamoDB.

Next, let's set up pre-requisities.
