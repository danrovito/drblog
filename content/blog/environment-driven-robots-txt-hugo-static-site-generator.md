---
title: "Environment Driven Robots Txt Hugo Static Site Generator"
date: 2020-02-21T23:23:04-05:00
draft: false
description: "Here is an easy way to block your sites from search engines when using Hugo.  Easily blog search engines by using environment variables."
tags: ["Hugo"]
keywords: ["hugo", "static", "netlify", "robots.txt"]
timage: "images/robots-image.jpg"
identifier: 23add932-b240-4c32-80f4-3d179405ab10
---

Sometimes when you deploy a project you may have to block search engines.  Maybe it's a development site, maybe its not ready, or maybe you just don't want search engines to access your site.  

Whatever the case may be here is a simple way to use environment variables in Hugo and Netlify.  You won't have to think about it again. Just set it and forget it.

#### Hugo

Start off by adding the following to your `config.toml` in Hugo:

```
enableRobotsTXT = true
```

After this you'll need to add a `robots.txt` file.  Create this file in the following area:

```
/layouts/robots.txt
```

Inside your `robots.txt` file add the following code:

```
User-agent: *
Disallow: {{ if ne (getenv "APPENV") "production" }}/{{ end }}
```

### Netlify

Now, head over to netlify and on your site go to `Settings>Build & Deploy>Environment`.

![Netlify](/images/netlify-env.png)

Click `Edit Variables` then `New Variable`. 

Add the environment variable like the screenshot below:

![Netlify](/images/netlify-new-env.png)

After your next deploy you can head to `/robots.txt` and see your new file.  If the `APPENV` variable is set to something other than production you'll see:

```
User-agent: *
Disallow: /
```

If you have the `APPENV` variable set to `production` the file should read:

```
User-agent: *
Disallow:
```