---
title: 'Deploying an application using a Dockerfile'
chapter: true
weight: 25
pre: '<i class="fa fa-film" aria-hidden="true"></i> '
---

## Deploying to AWS App Runner with Docker

_Pre-requisites:_

This section of the workshop assumes you have docker installed. Follow the instructions at [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/).

Create a new directory “apprunner-example”, and in this directly, create the following files:

`index.js`

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

`package.json`

```json
{
  "name": "fusion_example",
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

`Dockerfile`

```dockerfile
FROM node:14

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./

RUN npm install

# Bundle app source
COPY . .

EXPOSE 3000
CMD [ "node", "index.js" ]
```

You should now have the following files in your directory:

```bash
iamtim@mypc:~/apprunner-example$ ls
Dockerfile  index.js  package.json
```
