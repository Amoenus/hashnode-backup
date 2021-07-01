## Turn Swagger Theme to the Dark Mode

So you have Swagger integrated into your .NET Core Web API application. Maybe even using my  [previous guide ](https://amoenus.dev/swagger-for-dotnet-core-webapi). And now you want to customize it a bit.

I prefer my UI’s dark. So, when I am presented with a predominantly white screen from the Swagger default theme, I immediately want to change it.
Luckily SwaggerUI supports CSS injection.

Here are the tweaks that we need to make:
## Changes for `Startup.cs`
### Enable support for static files in a `Configure()` method
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
    c.SwaggerEndpoint("/swagger/v1/swagger.json", "MyAPI");
    c.InjectStylesheet("/swagger-ui/SwaggerDark.css");
});
```
You’ve read till the end, so as a thank you here’s the link to the dark theme I just mentioned. It even comes with a dark scroll bar and custom drop-down arrows.
https://github.com/Amoenus/SwaggerDark/

Thank you for reading. Consider subscribing and leaving a comment.