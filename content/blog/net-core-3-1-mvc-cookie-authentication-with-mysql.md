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

This tutorial assumes you have a MySQL database installed and ready to use.

### Creating the Application

Open your Visual Studio 2019 with .Net Core 3.1 installed and select `Create a New Project`.  On the next screen select `ASP.NET Core Web Application`.

Name your project `Authentication` and save it at a location of your choosing.  My settings are as follows:


![Project Setup](/images/net-core-auth-post/pr-setup.png)

Press Create and on the next screen choose `Web Application (Model, View, Controller)` with No Authentication selected.

#### Required Packages

Before moving forward we need to install some required packages.  In your Package Manager Console run the following commands:

```plaintext
Install-Package Pomelo.EntityFrameworkCore.MySql
Install-Package Microsoft.EntityFrameworkCore.Design
Install-Package Microsoft.EntityFrameworkCore.Tools
```

### Startup.cs

Open your `Startup.cs` file.  The method we'll be working in is the `ConfigureServices` method. Which should look like this:

```c#
public void ConfigureServices(IServiceCollection services)
{
    services.AddControllersWithViews();
}    
```