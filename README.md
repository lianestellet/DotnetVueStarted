# Dotnet Vue Started

This was an experimental project to show how we could integrate vue on Razor Mvc.

Prerequisites:
* NPM - Need to have npm installed
* dotnet core - Need dotnet core 2.1 installed 
* webpack -  need to install webpack

instructions:
* npm install
* dotnet restore
* dotnet build
* dotnet run

> VueApp - put your vue application here, I used a sample exercise from my repo: https://github.com/pablostellet/vue-web-apps-trial

 Changes in project to make it work:

1- At your **Startup.cs** file, use this middleware to run webpack at dotnet run.

 ```
using Microsoft.AspNetCore.SpaServices.Webpack;
...

public void Configure(IApplicationBuilder app, IHostingEnvironment env) {
    if (env.IsDevelopment())
    {
        app.UseBrowserLink();
        app.UseDeveloperExceptionPage();
        // add middleware here
        app.UseWebpackDevMiddleware(new WebpackDevMiddlewareOptions
    {
        HotModuleReplacement = true
    });
}
 ```

**also add this SPA route:**
```
app.UseMvc(routes =>
{
    routes.MapRoute(
        name: "default",
        template: "{controller=Home}/{action=Index}/{id?}");

    routes.MapSpaFallbackRoute("spa-fallback", new { controller = "Home", action = "Index" }); 

});
```



2- create **.babelrc** on root using this piece of code for transpilling es6 files:

```
{
	"presets": ["es2015", "stage-2"]
}
```

3- Add the **package.json** file to manage dependencies

4- Add **webpack.config.js** file to bundle the Vue application and generate a single file that will be loaded on the application page

_NOTE: "The main webpack role on this example, is to bundle the vue and js files into a compatible js file. Take a look at entry and output files."_

*steps 3 and 4 could be done easier using the commands:

1- *npm init* 

2- *webpack init*

or if you have vue-client installed (*npm i vue-cli -g*):
*vue init webpack-simple VueApp*

Each way it's a good thing to understand how it's done gradually. Credits for David Katz that created an awesome Vue.js course at udemy.

