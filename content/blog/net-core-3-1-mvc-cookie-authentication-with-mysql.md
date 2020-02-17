---
title: ".Net Core 3.1 MVC Cookie Authentication with MySQL"
description: ""
date: 2020-02-17T13:56:38-05:00
draft: false
tags: ["Development", "Node"]
keywords: ["nodejs", "api", "javascript"]
timage: "https://placehold.it/1920x1080"
identifier: c3404b69-2392-4506-8e21-ea95649c1dcc
---

Creating an authentication system for .Net Core can be as simple as selecting `Individual User Accounts` like shown below.

![Individual Accounts](/images/net-core-auth-post/user-accounts.png)

What if we want to go beyond this and use a different solution that isn't Identity?  In this tutorial, we'll go over how to implement cookie based authentication in a .Net Core 3.1 project.  We'll also be connecting our project to MySQL to store our user information.

This tutorial assumes you know how to setup a .Net Core 3.1 MVC Project.  It also assumes you have a MySQL database installed and ready to use.