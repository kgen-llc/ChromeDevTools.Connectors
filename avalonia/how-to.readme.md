### How to add Avalonia ChromeDevTools Connector for your application


Step 1 : reference the nuget package
``` <PackageReference Include="kgen.ChromeDevToolsConnector.Avalonia" Version="0.1.1" />

Step 2: enable the usage and your custom configuration

Note: you MUST enable Avalonia.Diagnostics.Diagnostic.IsEnabled Switch
See ___EnableChromeDevToolsConnector___ call with the different configuration  
```
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
Step 3:
Use it !

