---
title: "Build a Rest API With Node.js, Express, and MongoDB"
description: "Building a Rest API with Node.js is a very exciting way to consume data.  In this tutorial we will combine a few packages from npm as well as write some structured code to tell our API what to do."
date: 2020-02-04T08:57:09-05:00
draft: false
tags: ["Development", "Node"]
keywords: ["nodejs", "api", "javascript"]
timage: ""
identifier: eiwtr09i430
---

Building a Rest API with Node.js is a very exciting way to consume data.  In this tutorial we will combine a few packages from npm as well as write some structured code to tell our API what to do.  At the end of the tutorial, we will have a fully functional API that reads, writes, and updates to our MongoDB database.


#### Getting Started

First, we'll need to begin our project.  Let's start by running the following command inside the root folder of our project using our terminal:

```plaintext
npm init
```

While we are here let's alos install our packages we'll use via `npm`

```plaintext
npm install body-parser cors dotenv express mongoose nodemon
```

This will install the following

 - [Body-Parser](https://www.npmjs.com/package/body-parser)
 	- Parse incoming request bodies in a middleware before your handlers
 - [Cors](https://www.npmjs.com/package/cors)
 	- CORS is a node.js package for providing a Connect/Express middleware that can be used to enable CORS with various options.
 - [Dotenv](https://www.npmjs.com/package/dotenv)
 	- A zero-dependency module that loads environment variables from a .env file into process.env
 - [Express](https://www.npmjs.com/package/express)
 	- Fast, unopinionated, minimalist web framework
 - [Mongoose](https://www.npmjs.com/package/mongoose)
 	- A MongoDB object modeling tool designed to work in an asynchronous environment.
 - [Nodemon](https://www.npmjs.com/package/nodemon)
 	- A tool that helps develop node.js based applications by automatically restarting the node application when file changes in the directory are detected.

#### Create app.js

Create a new file in our project root called `app.js`.  This will be our starting point for our API.  We'll start by requiring our packages that we imported earlier.

```javascript
const express = require('express');
const app = express();
const mongoose = require('mongoose');
const bodyParser = require('body-parser');
const cors = require('cors');

require('dotenv/config');
```

CORS (Cross-Origin Resource Sharing) is required so that our API can be accessed by other applications from a different origin.

