---
title: 'Connect AWS App Runner to GitHub'
chapter: true
weight: 12
---

# Connect AWS App Runner to GitHub

In the service creation console walk-through Step 1, you will be prompted for a number of inputs,
let's walk them through.

First, for _repository type_, select _"Source code repository"_, this will tell AWS App Runner to
use a source code repostiory as the source for our deployments. It will require us to connect AWS
App Runner with GitHub, so let's go ahead and do that!

![Source Service](/images/service-source.png)

In the _Connect to GitHub_ section, click _Add new_ to create a new connection to GitHub.

![Add New](/images/service-github-add-new-connection.png)

A popup window should appear prompting you to input some additional details for your GitHub
connection. Give the connection a suitable name, for example `apprunner-example-connection`. Install
a GitHub app with access to the repository you have previously forked by choosing the username to
which you created your repository.

![Github Link](/images/service-link-github1.png)

![Github Link](/images/service-link-github2.png)

Confirm your password

![Github Link](/images/service-link-github3.png)

Select the repository you forked earlier within “Only select repositories”, and click “Save”. You
will now be taken back to Step 1 within AWS App Runner service creation.

![Github Link](/images/service-link-github4.png)

Great, we have now connected AWS App Runner to GitHub, so that it can fetch the source code of our
forked repository and deploy it, let's move on to the next step.
