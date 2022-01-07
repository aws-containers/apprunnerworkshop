---
title: 'Introduce a change to our app'
chapter: true
weight: 14
---

# Automatic deployment on code change

In this section, we will introduce a change to app, and see how AWS App Runner automatically
identifies the change to our code, and builds and deploys the new version.

## Edit a template

Browse to https://github.com/[YOUR_GITHUB_USER]/repostatus-gh-demo/edit/main/templates/repo.html to
get a browser editor. You should see something similar to the below

![GitHub editor](/images/intermediate/github-editor.png)

Let's change the appearance of our app by making the text bold, wrap the text in the template with
`<b>` and `</b>`, so that you end up with `<b>This is the page for repostiory: {{ repo.repo_slug }}, contains data: {{ repo.data }}</b>`

![GitHub editor](/images/intermediate/github-commit-change.png)

Click _Commit changes_.

## Validate the deployment

Shortly after commiting the changes to your repository, AWS App Runner will start a new deployment
activity. Go to _Services -> apprunnerworkshop-app_ in the AWS App Runner console.

![AppRunner Deployment](/images/intermediate/deployment-activity.png)

And you should see a new activity related to the change you just introduced.

When the status of our `apprunnerworkshop-app` service changes from _Operation in progress_ to
_Running_, we can have a look at our changes by browsing to `https://[DOMAIN_HERE]/repo/[YOUR_GITHUB_USERNAME]/repostatus-gh-demo`,
where we should now see the text in a bold font.
