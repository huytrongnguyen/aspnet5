# ASP.NET MVC6
## The MVC Pattern
* Model–view–controller (MVC) is a software architecture pattern
* Originally formulated in the late 1970s by Trygve Reenskaug as part of the Smalltalk
* Code reusability and separation of concerns
* Originally developed for desktop, then adapted for internet applications

## MVC Steps
* Incoming request routed to Controller
  * For web: HTTP request
* Controller processes request and creates presentation Model
  * Controller also selects appropriate result (view)
* Model is passed to View
* View transforms Model into appropriate output format (HTML)
* Response is rendered (HTTP Response)

## The ASP.NET MVC History
* ASP.NET MVC 1.0
  * In February 2007, Scott Guthrie ("ScottGu") of Microsoft sketched out the core of ASP.NET MVC
  * Released on 13 March 2009
* ASP.NET MVC 2.0 (Areas, Async)
  * Released just one year later, on 10 March 2010
* ASP.NET MVC 3.0 (Razor) – 13 January 2011
* ASP.NET MVC 4.0 (Web API) – 15 August 2012
* ASP.NET MVC 5.0 (Identity) – 17 October 2013
* ASP.NET MVC 6.0 – beta

## ASP.NET MVC Routing
* Mapping between patterns and a combination of controller + action + parameters
* Register routes

```csharp
// Configure is called after ConfigureServices is called.
public void Configure(IApplicationBuilder app) {
  // Add static files to the request pipeline.
  app.UseStaticFiles();

  // Add MVC to the request pipeline.
  app.UseMvc(routes => {
    routes.MapRoute("default", "{controller=Home}/{action=Index}/{id?}");
    routes.MapRoute("area", "{area}/{controller=Home}/{action=Index}/{id?}");
    routes.MapRoute("api", "api/{controller=Values}/{id?}");
  });
}
```

## Controllers
* The core component of the MVC pattern
* All the controllers should be available in a folder by name Controllers
* Controller naming standard should be "nameController" (convention)
* Routers instantiate controllers in every request
* All requests are mapped to a specific action
* Every controller should inherit Controller class

## Actions
* Actions are the ultimate request destination
  * Public controller methods
  * Non-static
  * No return value restrictions
* Actions typically return an IActionResult 

## Action Parameters
* ASP.NET MVC maps the data from the HTTP request to action parameters in few ways:
  * Routing engine can pass parameters to actions
    * http://localhost/Users/Lionel
    * Routing pattern: Users/{username}
  * URL query string can contains parameters
    * /Users/ByUsername?username=Lionel
  * HTTP post data can also contain parameters

