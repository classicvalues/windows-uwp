---
title: Create your first WinUI 3 project
description: In this topic we'll see how to use Visual Studio to create a new project for a C# .NET or C++ app that has a [Windows UI Library (WinUI) 3](/windows/apps/winui/winui3/) user interface (UI). We'll also take a look at some of the code in the resulting project, what it does, and how it works.
ms.date: 03/10/2022
ms.topic: article
keywords: windows 11, windows 10, Windows App SDK, Windows app development platform, desktop development, win32, WinRT, uwp, toolkit sdk, winui, Windows UI Library, app sdk
---

# Create your first WinUI 3 project

In this topic we'll see how to use Visual Studio to create a new project for a C# .NET or C++ app that has a [Windows UI Library (WinUI) 3](/windows/apps/winui/winui3/) user interface (UI). We'll also take a look at some of the code in the resulting project, what it does, and how it works.

Links to full installation details are in the steps below. We recommend the Windows App SDK version 1.0 Stable, but you can choose any version from any of the [Windows App SDK release channels](/windows/apps/windows-app-sdk/release-channels). From that topic, you can follow the links to the release notes for each channel. Be sure to check any *limitations and known issues* in the release notes, since those might affect the results of following along with these steps.

[!INCLUDE [UWP migration guidance](../../windows-app-sdk/includes/uwp-app-sdk-migration-pointer.md)]

## Key concepts

[!INCLUDE [Packaged apps, Unpackaged apps](../../windows-app-sdk/includes/glossary/packaged-unpackaged-include.md)]

## Packaged: Create a new project for a packaged C# or C++ WinUI 3 desktop app

1. To set up your development computer, see [Install tools for the Windows App SDK](/windows/apps/windows-app-sdk/set-up-your-development-environment).

1. In Visual Studio, select **File** > **New** > **Project**.

1. In the **New Project** dialog's drop-down filters, select **C#**/**C++**, **Windows**, and **WinUI**, respectively.

1. Select the **Blank App, Packaged (WinUI 3 in Desktop)** project template, and click **Next**. That template creates a desktop app with a WinUI 3-based user interface. The generated project is configured with the package manifest and other support needed to build the app into an MSIX package (see [What is MSIX?](/windows/msix/overview)). For more information about this project template, see [Package your app using single-project MSIX](/windows/apps/windows-app-sdk/single-project-msix).

    :::image type="content" source="images/WinUI3-csharp-newproject-1.0-later.png" alt-text="Screenshot of Create a new project wizard with the Blank App Packaged (Win UI in Desktop) option highlighted." lightbox="images/WinUI3-csharp-newproject-1.0-later.png":::

1. Enter a project name, choose any other options as desired, and click **Create**.

1. The project that Visual Studio generates contains your app's code. The **App.xaml** file and code-behind file(s) define an **Application**-derived class that represents your running app. The **MainWindow.xaml** file and code-behind file(s) define a **MainWindow** class that represents the main window displayed by your app. Those classes derive from types in the **Microsoft.UI.Xaml** namespace provided by WinUI 3.

    The project also includes the package manifest for building the app into an [MSIX package](/windows/msix/overview).

    ![Screenshot of Visual Studio showing the Solution Explorer pane and the contents of the Main Windows X A M L dot C S file for single project M S I X.](images/WinUI-csharp-appproject-1.0-later.png)

1. To add a new item to your app, right-click the project node in **Solution Explorer**, and select **Add** > **New Item**. In the **Add New Item** dialog box, select the **WinUI** tab, choose the item you want to add, and then click **Add**. For more details about the available items, see [WinUI 3 templates in Visual Studio](/windows/apps/winui/winui3/winui-project-templates-in-visual-studio).

    ![Screenshot of the Add New Item dialog box with the Installed > Visual C sharp Items > Win U I selected and the Blank Page option highlighted.](images/winui3-addnewitem.png)

1. Build and run your solution on your development computer to confirm that the app runs without errors.

## Unpackaged: Create a new project for an unpackaged C# or C++ WinUI 3 desktop app

1. To set up your development computer, see [Install tools for the Windows App SDK](/windows/apps/windows-app-sdk/set-up-your-development-environment).

1. Use the button below to download the installer and MSIX packages for the Windows App SDK version 1.0 Stable runtime. Those are required to run and deploy an unpackaged app on a target device (see [Windows App SDK deployment guide for unpackaged apps](/windows/apps/windows-app-sdk/deploy-unpackaged-apps)).

    > [!div class="button"]
    > [Microsoft.WindowsAppRuntime.Redist.1.0.0.zip](https://aka.ms/windowsappsdk/1.0-stable/msix-installer)

1. **C++**. Install the [Microsoft Visual C++ Redistributable (VCRedist)](/cpp/windows/latest-supported-vc-redist) appropriate for the architecture of the target device.

    - The latest version of the VCRedist is compatible with the latest Visual Studio generally-available (GA) release (that is, not preview), as well as all versions of Visual Studio that can be used to build Windows App SDK binaries.
    - Insider builds of Visual Studio might have installed a later version of the VCRedist, and running the public version will then fail with this error (which you can ignore): **Error 0x80070666: Cannot install a product when a newer version is installed.**

    > [!NOTE]
    > If you don't have the VCRedist installed on the target device, then dynamic links to `c:\windows\system32\vcruntime140.dll` fail. That failure can manifest to end users in various ways.

1. In Visual Studio, select **File** > **New** > **Project**.

1. In the New Project dialog's drop-down filters, select **C#**/**C++**, **Windows**, and **WinUI**, respectively.

1. You need to start with a packaged project in order to use XAML diagnostics. So select the **Blank App, Packaged (WinUI 3 in Desktop)** project template, and click **Next**. .

1. Add the following property to your project file&mdash;either your `.csproj` (C#) or `.vcxproj` (C++) file:

   ```xml
   <WindowsPackageType>None</WindowsPackageType>
   ```

    :::image type="content" source="images/winui-csharp-unpackaged-proj.png" alt-text="Visual Studio 2019 - C# Project file with WindowsPackageType set to None highlighted":::

1. **C++**. In your C++ project (`.vcxproj`) file, set the *AppxPackage* property to *false*:

   ```xml
    <AppxPackage>false</AppxPackage>
   ```

1. **C#**. To start a C# app from Visual Studio (either **Debugging** or **Without Debugging**), select the *Unpackaged* launch profile from the **Start** drop-down. If the *Package* profile is selected, then you'll see a deployment error in Visual Studio. This step isn't necessary if you start the application (`.exe`) from the command line or from Windows File Explorer.
  
      :::image type="content" source="images/winui3-csharp-launch-profile.png" alt-text="Visual Studio - Start drop-down with C# application unpackaged launch profile highlighted":::

1. Build and run.

Instead of setting the **WindowsPackageType** project property to *None*, you can use the bootstrapper API (see [Reference the Windows App SDK framework package at run time](/windows/apps/windows-app-sdk/reference-framework-package-run-time) to initialize the [Bootstrapper](/windows/apps/windows-app-sdk/deployment-architecture#bootstrapper). For more details on that option, see [Build and deploy an unpackaged app](/windows/apps/windows-app-sdk/tutorial-unpackaged-deployment).

## A look at the code in the project template

In this walkthough, we used the **Blank App, Packaged (WinUI 3 in Desktop)** project template, which creates a desktop app with a WinUI 3-based user interface. Let's take a look at some of the code that comes with that template, and what it does. For more info on available WinUI 3 project and item templates, see [WinUI 3 templates in Visual Studio](/windows/apps/winui/winui3/winui-project-templates-in-visual-studio).

### The app's entry point

When the Windows operating system (OS) runs an app, the OS begins execution in the app's *entry point*. That entry point takes the form of a **Main** (or **wWinMain** for C++/WinRT) function. Ordinarily, a new project configures that function to be auto-generated by the Visual Studio build process. And it's hidden by default, so you don't need to be concerned with it. But if you *are* curious for more info, then see [Single-instancing in Main or wWinMain](/windows/apps/windows-app-sdk/migrate-to-windows-app-sdk/guides/applifecycle#single-instancing-in-main-or-wwinmain).

### The App class

The app as a whole is represented by a class that's typically called simply **App**. That class is defined in **App.xaml** and in its code-behind file(s) (`App.xaml.cs`, or `App.xaml.h` and `.cpp`). **App** is derived from the WinUI 3 [**Microsoft.UI.Xaml.Application**](/windows/winui/api/microsoft.ui.xaml.application) class.

The generated code in the entry point creates an instance of **App**, and sets it running.

In the constructor of **App**, you'll see the **InitializeComponent** method being called. That method essentially parses the contents of **App.xaml**, which is XAML markup. And that's important because **App.xaml** contains merged resources that need to be resolved and loaded into a dictionary for the running app to use.

Another interesting method of **App** is **OnLaunched**. In there we create and activate a new instance of the **MainWindow** class (which we'll look at next).

### The MainWindow class

The main window displayed by the app is of course represented by the **MainWindow** class. That class is defined in **MainWindow.xaml** and in its code-behind file(s) (`MainWindow.xaml.cs`, or `MainWindow.xaml.h` and `.cpp`). **MainWindow** is derived from the WinUI 3 [**Microsoft.UI.Xaml.Window**](/windows/winui/api/microsoft.ui.xaml.window) class.

The constructor of **MainWindow** calls its own **InitializeComponent** method. Again, its job is to turn the XAML markup inside **MainWindow.xaml** into a graph of user interface (UI) objects.

In **MainWindow.xaml** you'll see the basic layout of **MainWindow**. At the layout root is a dynamic panel called a [**Microsoft.UI.Xaml.Controls.StackPanel**](/windows/winui/api/microsoft.ui.xaml.controls.stackpanel). For more info about layout panels, see [Layout panels](/windows/apps/design/layout/layout-panels).

Inside that **StackPanel** is a [**Microsoft.UI.Xaml.Controls.Button**](/uwp/api/windows.ui.xaml.controls.button). And that **Button** uses the markup `Click="myButton_Click"` to declaratively hook up an event handler method for the [**Click**](/uwp/api/windows.ui.xaml.controls.primitives.buttonbase.click) event.

That method is named **myButton_Click**, and you can find the implementation of that method in `MainWindow.xaml.cs`, or in `MainWindow.xaml.cpp`. In it, the content of the button is changed from the default "Click Me" to "Clicked".

**C++**. If you created a C++ project, then you'll also see a `MainWindow.idl` file. For more info, see the [C++/WinRT](/windows/uwp/cpp-and-winrt-apis/) documentation. [XAML controls; bind to a C++/WinRT property](/windows/uwp/cpp-and-winrt-apis/binding-property) is a good place to start learning about the purpose and usage of `.idl` files.

## Next steps

To continue your development journey with the Windows App SDK, see [Develop Windows desktop apps](/windows/apps/develop/).

## Related topics

* [Windows UI Library (WinUI) 3](/windows/apps/winui/winui3/)
* [Windows App SDK release channels](/windows/apps/windows-app-sdk/release-channels)
* [Install tools for the Windows App SDK](/windows/apps/windows-app-sdk/set-up-your-development-environment)
* [What is MSIX?](/windows/msix/overview)
* [Package your app using single-project MSIX](/windows/apps/windows-app-sdk/single-project-msix)
* [WinUI 3 project templates in Visual Studio](/windows/apps/winui/winui3/winui-project-templates-in-visual-studio)
* [Windows App SDK deployment guide for unpackaged apps](/windows/apps/windows-app-sdk/deploy-unpackaged-apps)
* [Microsoft Visual C++ Redistributable (VCRedist)](/cpp/windows/latest-supported-vc-redist)
* [Reference the Windows App SDK framework package at run time](/windows/apps/windows-app-sdk/reference-framework-package-run-time)
* [Deployment architecture for the Windows App SDK](/windows/apps/windows-app-sdk/deployment-architecture)
* [Build and deploy an unpackaged app](/windows/apps/windows-app-sdk/tutorial-unpackaged-deployment)
* [Develop Windows desktop apps](/windows/apps/develop/)
