## How to integrate Swagger UI in a .NET Core Web API application | Amoenus Dev

[Swagger](https://swagger.io/) tooling allows you to generate beautiful API documentation, including a UI to explore and test operations, directly from your routes, controllers and models.
Setting it up is simple but requires some code changes.
To enable swagger integration for your .NET Core Web API project you will need to:
- Install Swashbuckle.AspNetCore package from NuGet
- Change the `Startup.cs` class of your Net Core Web API application.
   - Add using statement for `OpenApiInfo` 
   - Modify `Configure(IApplicationBuilder app, IWebHostEnvironment env)`
   - Modify `ConfigureServices(IServiceCollection services)`

## Changes for `Startup.cs`
### Installing Swagger
From your project folder install the Swagger Nuget package (5.5.1 for this instance)
```Terminal
dotnet add package Swashbuckle.AspNetCore.Swagger --version 5.5.1
```
### Using statement
```CSharp
using Microsoft.OpenApi.Models;
```
### Changes for `ConfigureServices()`
In the `ConfigureServices()` method you should add
```CSharp
services.AddMvc();
services.AddSwaggerGen(c =>
{
    c.SwaggerDoc(“v1”, new OpenApiInfo
    {
        Title = “My Awesome API”,
        Version = “v1”
    });
});
```
### Changes for `Configure()`
In the `Configure()` method you should add
```CSharp
app.UseSwagger();
app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint(“/ swagger / v1 / swagger.json”, “My Awesome API V1”);
});
```
I prefer to enable it only for development
```CSharp
if (env.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint(“/ swagger / v1 / swagger.json”, “My Awesome API V1”);
    });
}
```
## Taking it for a spin
After all these changes, we are finally ready to test our new integration.
```Terminal
dotnet run
```
Navigate to [localhost:4200/swagger](localhost:4200/swagger) to see the SwaggerUI 
> Note: your port may be different

## Bonus: Customisation
I prefer my UI’s dark. So, when I am presented with a predominantly white screen from the default theme, I immediately want to change it.
Luckily SwaggerUI supports CSS injection.

Here are the tweaks that we need to make
### Enable support for static files
```CSharp
app.UseStaticFiles();
```
### Add folder structure with custom CSS
```
wwwroot/
   └──swagger-ui/
      └── SwaggerDark.css
```
![Folder structure and location of SwaggerDark.css](https://cdn.hashnode.com/res/hashnode/image/upload/v1598982216244/9OHU5YoJd.png)
### Inject custom CSS
Now we can inject the custom CSS with `InjectStylesheet()`
```CSharp
app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint(“/ swagger / v1 / swagger.json”, “MyAPI”);
    c.InjectStylesheet(“/ swagger - ui / SwaggerDark.css”);
});
```
You’ve read till the end, so as a thank you here’s the link to the dark theme I mentioned. It even comes with a dark scroll bar and custom drop-down arrows.
https://github.com/Amoenus/SwaggerDark/

Did you have any questions or feedback? Please share them in the comments 🤗
