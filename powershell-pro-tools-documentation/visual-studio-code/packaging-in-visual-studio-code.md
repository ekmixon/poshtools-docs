---
description: Information about compiling PowerShell Scripts into executables with VS Code.
---

# Packaging in Visual Studio Code

{% hint style="info" %}
Requires [PowerShell Pro Tools](https://ironmansoftware.com/poshtools)
{% endhint %}

PowerShell Pro Tools provides an [extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ironmansoftware.powershellprotools). PowerShell Pro Tools takes advantage of the package.psd1 file to configure packaging for scripts within VS Code. 

## Requirements for Packaging

* PowerShell Pro Tools Visual Studio Code Extension
* .NET Core SDK 2.0 or later

## Compiling a Script 

To compile a script into an executable, open a PS1 file. In the top right of the toolbar, you will find a Package Script as Exe button. Clicking this button will start the packaging process. 

![Package Script as Exe Button](../../.gitbook/assets/image%20%2844%29.png)



If this is the first time you have clicked the button, a `package.psd1` file will be created in the current workspace's root. So for example, if you have the folder `C:\src\scripts` open in Visual Studio Code, the file `C:\src\scripts\package.psd1` will be created.

Next, the packaging process will start. The PowerShell Pro Tools Output Pane will be activated and will display log information about the packaging process.

![](../../.gitbook/assets/image%20%2843%29.png)

## Configuration Packaging

To configure packaging, you can change settings within the generated `package.psd1` file. You can learn more about the syntax of the file by [clicking here](../packaging/package.psd1.md).

The default configuration will look something like this. 

```text
@{
    Root = 'c:\Users\adamr\Desktop\test\test\test.ps1'
    OutputPath = 'c:\Users\adamr\Desktop\test\out'
    Package = @{
        Enabled = $true
        Obfuscate = $false
        HideConsoleWindow = $false
        DotNetVersion = 'v4.6.2'
        FileVersion = '1.0.0'
        FileDescription = ''
        ProductName = ''
        ProductVersion = ''
        Copyright = ''
        RequireElevation = $false
        ApplicationIconPath = ''
        PackageType = 'Console'
    }
    Bundle = @{
        Enabled = $true
        Modules = $true
        # IgnoredModules = @()
    }
}
```

### Root Package.psd1

The root `package.psd1` file is generated at the root of the current workspace folder. Here's an example of a file structure with a root `package.psd1` file. Clicking Package Script as Exe on an script will use this `package.psd1` file.

![](../../.gitbook/assets/image%20%2842%29.png)

### Scoped Package.psd1 

You can also include the `package.psd1` file in a particular folder. When packaging scripts in that folder, the scoped `package.psd1` file will be used. 

Take the following folder structure for example. 

![](../../.gitbook/assets/image%20%2840%29.png)

When packaging the `test\test.ps1` file, the `test\package.psd1` will be used to package the script. When packaging the `test2\test2.ps1` file, the `test\package.psd1` file will be used. The root `package.psd1` will used when packaging `test3\test3.ps1` because that folder does not have a scoped package config file. 

### Package.psd1 template

You can set the package.psd1 template that is used to create the default package.psd1 by setting the path to the file within your settings. 

![](../../.gitbook/assets/image%20%2822%29.png)

You can use two replacement variables that will be set when the file is created. 

**$root** - Replaced by the path to the PS1 file being packaged 

**$outputPath** - Path to the directory to output to. 



