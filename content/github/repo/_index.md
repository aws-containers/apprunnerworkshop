---
title: 'Setting up a Github repository'
chapter: true
weight: 10
pre: '<i class="fa fa-film" aria-hidden="true"></i> '
---

## Setting up a Github repository

Let’s get started by creating a new Private repository on GitHub - this can be done by logging into GitHub, and then visiting https://github.com/new.

![Create Repository](/images/github-new-repository.png)

Enter `simple-express-app` as your Repository name, and select “Private” in order to limit access to your repository. Click on “Create repository” in order to finalize creation.

![Create Repository](/images/github-new-file-1.png)

Next, we are going to create our two files in GitHub - start by selecting “creating a new file”:

![Create index.js](/images/github-create-index-js.png)

Choose a file name of `index.js`, and then paste in the following code below:

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`);
});
```

Select “Commit new file” in order to save this new file into your repository.

Next, we will create a `package.json` file in order to define our library dependencies:

![Create file](/images/github-package-json.png)

Click “Add file” to open a dropdown, and then select “Create new file”.

![Package json contents](/images/github-package-json-contents.png)

Paste the following code into the new file which you will name “package.json”

```json
{
  "name": "apprunner_example",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {},
  "author": "",
  "license": "ISC"
}
```

Select “Commit new file” in order to add this second file. We now have our repository prepared with a Node.js web service. For our next step, open the AWS console, and browse to the AWS App Runner service, or [https://console.aws.amazon.com/apprunner/home](https://console.aws.amazon.com/apprunner/home):

Your GitHub repository is now prepared. Proceed to the next section to run this repository using AWS App Runner.
