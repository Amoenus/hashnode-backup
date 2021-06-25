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
Now that you have Swagger configured, you might want to change the default theme.
You can learn how to do this in this  [blog post](https://amoenus.dev/swagger-dark-theme) 

Did you have any questions or feedback? Please share them in the comments 🤗
