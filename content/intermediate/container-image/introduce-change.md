---
title: 'Introduce a change to our app'
chapter: true
weight: 25
---

# Automatic deployment on code change

In this section, we will introduce a change to app, build a new version of our container image, and
see how AWS App Runner automatically the change, and deploys the new version.

## Change some code!

Let's introduce a change to our code that we will be able to visually inspect.

Open `templates/repo.html` in the Cloud9 editor, and change HTML formatting.

Before:

```
{% extends "base.html" %}

{% block body %}
This is the page for repostiory: {{ repo.repo_slug }}, contains data: {{ repo.data }}
{% endblock %}
```

After, with `<b>` and `</b>`:

```
{% extends "base.html" %}

{% block body %}
This is the page for repostiory: <b>{{ repo.repo_slug }}</b>, contains data: <b>{{ repo.data }}</b>
{% endblock %}
```

## Build a new image

Let's build a new image with our code changes:

```shell
$ cd ~/environment/repostatus-gh-demo
$ docker build -t apprunnerworkshop-app:demo .
[build output omitted]

$ docker tag apprunnerworkshop-app:demo $ECR_REPOSITORY_URI:demo
$ docker push $ECR_REPOSITORY_URI:demo
```

## Validate the deployment

Our service will now tranition into _Operation in progress_ while the deployment occurs, once it is
finished, the status will transtion to _Running_.

We can then validate that our deployment have succeeded, as we should now see a bold font when
visiting `https://[DOMAIN_HERE]/repo/[YOUR_GITHUB_USERNAME]/repostatus-gh-demo`.

![Deployed App](/images/intermediate/container-image/deployed-app.png)

That's it! We have deployed a new version of our app simply by pushing our newly built container
image.
