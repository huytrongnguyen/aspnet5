# ASP.NET 5 (vNext), MVC 6 and Entity Framework 7
## History of ASP (18 years)
* 1996 - Active Server Pages (ASP) 
* 2002 – ASP.NET
* 2008 – ASP.NET MVC
* 2010 – ASP.NET Web Pages
* 2012 – ASP.NET Web API, SignalR
* 2014 – ASP.NET 5

## What is Different in ASP.NET 5?
* Rebuild from ground up
* Request pipeline light and fast
* Cross-platform
* Host Anywhere
* Better Performance
* Middlewares & Custom Middleware
* Package Management
  * ASP.NET 5 introduces a new, lightweight way to manage dependencies in your projects
    * No more assembly references
    * Instead referencing NuGet packages
  * project.json file
* Other Improvements

## MVC + Web API + Web Pages = ASP.NET MVC 6!
* MVC, Web API, and Web Pages are merged into a single framework called MVC 6
* Solution layout

![MVC 6 Template](https://github.com/huytrongnguyen/aspnet5/blob/master/css/imgs/mvc6-template.png)

* MVC 6 Root files
  * JSON configurations + CSharp 
  * Bower: JS + CSS frameworks
  * Config: settings, connections
  * Gulpfile: client build tasks
  * Package: package versions
  * Project: dependencies, secrets, commands, frameworks, excludes, scripts
  * Startup: initialization code
