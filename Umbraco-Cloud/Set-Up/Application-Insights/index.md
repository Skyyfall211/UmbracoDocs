---
versionFrom: 9.0.0
---

# Application Insights on Umbraco cloud

## Installing application Insights

This guide will instruct you how to install Application Insights (AI) for your cloud solution.

### Azure portal

First thing to have in place when installing AI is an AI resource on Azure, so go ahead and open your favorite browser and log onto the [Azure Portal](https://portal.azure.com) and spin up a new AI Resource.

After that, you can go ahead and grab your `instrumentation key`, from the AI Resource overview

![alt text](images/01-Instrumentation-key.png "Instrumentation Key")

### Cloud solution

The next thing we need to look at is how to enable AI for your Umbraco solution.

The easiest way is to open the command prompt of your choice and run the following command:

`dotnet add package Microsoft.ApplicationInsights.AspNetCore`

This will install Application Insights and all of its dependencies. Open the `appSettings.json` file and paste in your `instrumentation key` found in the previous section.

```json
"ApplicationInsights": {
    "InstrumentationKey": "your_key_here"
  },
```

Last step is to enable Application Insights in your application. You can achieve this by updating the `Startup.cs` class.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddUmbraco(_env, _config)
        .AddBackOffice()
        .AddWebsite()
        .AddComposers()
        .Build();

    // The following line enables Application Insights telemetry collection.
    services.AddApplicationInsightsTelemetry();
}
```

Upload the changes to your solution and that is it!

## Application Insights limitations on Umbraco Cloud

Unless you have a dedicated Umbraco Cloud server, you are sharing resources with other Umbraco Cloud users. By default Application Insights is configured to provide information about resources allocated and used by the system, do note however that these can be a misrepresentation!

## Microsoft documentation

For further information check out Microsoft's own documentation of [Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)
