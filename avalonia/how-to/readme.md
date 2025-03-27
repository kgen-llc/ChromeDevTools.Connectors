# How to add Avalonia ChromeDevTools Connector for your application

***Disclaimer: The versions available on nuget.org are free for usage but contains telemetry enabled by default using plausible.io.***
Please contact us for binar version without temetry or source access at [tech@kgen-llc.com](mailto:tech@kgen-llc.com).

## Step 1 : reference the nuget package

```xml
<PackageReference Include="kgen.ChromeDevToolsConnector.Avalonia" Version="0.2.0" />
```

*Note: At the moment a nightly build from Avalonia is required. you will need to use a ***11.3.\*-\**** version of Avalonia.*

## Step 2: enable the usage and your custom configuration

1. enable Avalonia Diagnostics via Avalonia.Diagnostics.Diagnostic.IsEnabled switch
2. Call *EnableChromeDevToolsConnector*  with your own configuration

You can configure on which port the chrome connecotr is running, the name to display and the favIconUrl when displayed into the chrome://inspect window
You can also configure which are you would like to monitor. It is recommended to keep it null for the basic uses cases and do the filtering into the chrome UI.

```csharp
public sealed class Program
{
    [STAThread]
    public static void Main(string[] args) {
        AppContext.SetSwitch("Avalonia.Diagnostics.Diagnostic.IsEnabled", true);
        
        BuildAvaloniaApp()
        .StartWithClassicDesktopLifetime(args);
    }
    // Avalonia configuration, don't remove; also used by visual designer.
    public static AppBuilder BuildAvaloniaApp()
        => AppBuilder.Configure<App>()
                .EnableChromeDevToolsConnector(new (
                    Port: 12345, ProductName: "my product",
                    favIconUrl: null), 
                    areas: null)
            .UsePlatformDetect()
            .WithInterFont();
}
```

And that's it !
This can be easily ntegrated into your application behind a flag to be enabled at startup.
Even if the Avalonia Switch is having a minimal impact, we recommend you to only enable both switch and the connector when required.

## Step 3 : Use it

See our [Demo app documentation](../demo-app/readme.md)
