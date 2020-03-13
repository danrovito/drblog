---
title: "Customizing Identity Table Names in .Net Core 3.1"
date: 2020-03-13T09:02:11-04:00
draft: false
description: "Customizing the default identity tables is a simple task making them more readable and easier to use in your application."
tags: [".net core"]
keywords: ["identity", "core", "3.1", ".net"]
timage: "/images/identity-tables.jpg"
identifier: bfeaa21b-06b3-40f8-be00-7a4731c88780
comments: open
---

Customizing the default table table names in Identity can seem like an overwhelming task.  Luckily, it's very simple.  We can follow a few easy steps to have our table names be readable and easier to use in our application.

Having your tables named "AspNetUsers" or similar can be very frustrating to look at.  Being able to customize these names will help our code look nicer, stay organized, and follow general naming conventions of our tables.

##### DB Context

The first step is to add some code to our applications DB Context.  In this case our class is called `ApplicationDbContext`.

The first thing we'll do is add an override to our `OnModelCreating` method.

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    // Override default AspNet Identity table names
    modelBuilder.Entity<User>(entity 
        => { entity.ToTable(name: "Users"); });
    modelBuilder.Entity<IdentityRole>(entity 
        => { entity.ToTable(name: "Roles"); });
    modelBuilder.Entity<IdentityUserRole<string>>(entity 
        => { entity.ToTable("UserRoles"); });
    modelBuilder.Entity<IdentityUserClaim<string>>(entity 
        => { entity.ToTable("UserClaims"); });
    modelBuilder.Entity<IdentityUserLogin<string>>(entity 
        => { entity.ToTable("UserLogins"); });
    modelBuilder.Entity<IdentityUserToken<string>>(entity 
        => { entity.ToTable("UserTokens"); });
    modelBuilder.Entity<IdentityRoleClaim<string>>(entity 
        => { entity.ToTable("RoleClaims"); });
}
```

This will chagne our table names to the string within the `ToTable`.

For example, this line turns the AspNetUsers table into Users:

```cs
modelBuilder.Entity<User>(entity => { entity.ToTable(name: "Users"); });
```

We'll also need to inherit from `IdentityDbContext`.  For this we'll have to add the inheritance to our `ApplicationDbContext` class

```cs
public class ApplicationDbContext : IdentityDbContext<User>
```

##### User Model

In the above section we reference a User class in a few spots.  This is our user model that can be used to customize columns in our user table.  For this we'll need to create a new model.

In your Models folder add a new class called `User.cs`.  In this class we'll be inheriting from the `IdentityUser`.

```cs
public class User : IdentityUser
{
    //Additional properties for your table would go here
}
```

The last piece of this change is that anywhere you would have used `IdentityUser` you will have to change that to `User`.  An example of where this change needs to take place is in `Views/Shared/_LoginPartial.cshtml`.  The current `@inject` would need the model being called to be changed to User.

```cs
@inject SignInManager<User> SignInManager
@inject UserManager<User> UserManager
```

If you are using the scaffolded items from identity you'll also want to check within those for lines such as

```cs
private readonly UserManager<User> _userManager;
private readonly SignInManager<User> _signInManager;
```