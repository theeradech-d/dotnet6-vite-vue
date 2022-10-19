# dotnet 6 & vite vue

## Step 1 - create .NET project

```shell
dotnet new react -o MyProjectName
```

## Step 2 - create Vue 3 project

```shell
npm create vite@latest
```

enter 

project name `ClientApp`

select `vue`

## Step 3 - Configure proxying

### Remove the SPA Proxy package

file `Properties/launchSettings.json`

remove line

```
"ASPNETCORE_HOSTINGSTARTUPASSEMBLIES": "Microsoft.AspNetCore.SpaProxy"
```

file `appsettings.Development.json`

remove line

```
"Microsoft.AspNetCore.SpaProxy": "Information",
```

file `.csproj`

remove line

```
<SpaProxyServerUrl>https://localhost:44476</SpaProxyServerUrl>
```
```
<SpaProxyLaunchCommand>npm start</SpaProxyLaunchCommand>
```
```
<PackageReference Include="Microsoft.AspNetCore.SpaProxy" Version="6.0.4" />
```

## Remove nuget package
```
Microsoft.AspNetCore.SpaProxy
```

## Add nuget package

```
Microsoft.AspNetCore.SpaServices.Extensions
```


file `Program.cs`

```
// START ADD -----------------

app.UseEndpoints(endpoints =>
{
    endpoints.MapControllerRoute(
        name: "default",
        pattern: "{controller}/{action=Index}/{id?}"
    );
});

if (app.Environment.IsDevelopment())
{
    app.UseSpa(spa =>
    {
        spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    });
}
else
{
    app.MapFallbackToFile("index.html");
}
// END ADD -----------------

app.Run();
```

## run vite
```
cd ClientApp
```
```
npm run dev
```

## run dotnet
```
dotnet watch
```