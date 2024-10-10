# Starting A Mod

> **INFO**
>
> This tutorial is taken and adapted from the [Lethal Company Modding Wiki](https://lethal.wiki). For more resources refer to that.
>

## Setting up your project
> **WARNING**
> 
> This guide assumes you've completed all the required steps in [initial setup](Initial-Setup.md), or that you know what you're doing.
> 
{style="warning"}
This guide follows certain parts of the [official BepInEx guide](https://docs.bepinex.dev/articles/dev_guide/plugin_tutorial/2_plugin_start.html) and the [Lethal Company Modding Wiki](https://lethal.wiki/dev/starting-a-mod).

### Using the dotnet template
First things first, you'll need to create your project. If you've not done so already, I recommend running the following command in a console to add some Content Warning templates for new projects:

```shell
dotnet new install Xilophor.ContentWarningTemplates
```

Next, you'll want to create a new project (sometimes called "solution", in C#). There are two main ways to do this.

**Using an IDE (easier)**

Depending on your IDE, this process will look slightly different. You'll want to give the solution the name of your soon-to-be mod. If given the option to use a template (you may want to google for "how to use template in Visual Studio" or "how to use template in Rider"), use the ``Content Warning Harmony Mod Template`

** Using the console (recommended for control)
Alternatively, you can open a console and run the following command, assuming you've set up the templates using the command above. Replace MyFirstMod with your mod's name, and MyName with your username:

```shell
dotnet new cwharmony -n MyFirstMod -M MyName.MyFirstMod
```

To see the other options provided in the mod template, you can use the following command:

```shell
dotnet new cwharmony --help
```

**Note for MonoMod users**

#### MonoMod Template {collapsible="true"}
> If you want to use MonoMod, you can instead use the Content Warning MonoMod Mod Template in your IDE or use cwmonomod instead of cwharmony in the console.
>
> This template has an additional argument/setting required for MonoMod specifically. In VS, it can be seen under Plugins Directory, and in the console, it's set with the ``-P`` argument. This argument/setting is to set the HookGen directory to use for hooking.
>
> Example command line usage with a path of
> ``C:\path\to\r2modmanPlus-local\ContentWarning\test\BepInEx\plugins\``:
> 
> ```shell
> dotnet new cwmonomod -n MyFirstMod -M MyName.MyFirstMod -P "C:\path\to\r2modman-local\ContentWarning\test\BepInEx\plugins\"
> ```
{style="tip"}

# Fixing an issue

Currently the Content Warning game assemblies may not be functional. You can test this by going to your project's main CS file and typing at the top:
```
using Zorro;
```
If it does not give an error, you may skip this section.

To fix this, open your csproj file by double-clicking it.

![CSProj Display](csproj1.png)

Then locate the highlighted line, and cut (CTRL + X) it:

![CSProj Display](csproj2.png)

Finally, paste it into the highlighted position:

![CSProj Display](csproj3.png)

Then you can save and close out of the csproj file, because you've fixed it! Now retry the first step in this section. If it doesn't give an error, then you're done here.

## "Building" your mod
Your IDE is capable of turning your code into a file that can be run (in this case by BepInEx as a mod). This process is called "building" or "compiling". In this case, it will turn your code into a ``.dll`` file. This file is your mod.

Depending on your IDE, the build button may be placed differently.

#### Visual Studio {collapsible="true"}
> For Visual Studio, it is the green arrow button with your project name:
> 
> ![VS Build button](visualstudiobuild.png)
> 
> Alternatively, you can press CTRL + Shift + B to build.
> 
{style="tip"}
#### Rider {collapsible="true"}
> For Rider, it is the hammer icon in the top right:
>
> ![Rider Build button](riderbuild.png)
>
{style="tip"}
#### VS Code {collapsible="true"}
> VS Code has no built-in way of building a C# project, as VS Code is a lightweight code editor and not an IDE. In order to build a C# project, you instead have to download the [C# Dev Kit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit) extension.
>
> After installing the extension, you can build by pressing ``Ctrl+Shift+P``, typing in Build and selecting ``.NET: Build``.
> 
> ![VSC Build](net-build-command.gif)
>
{style="tip"}

Once built, you should be able to find the ``.dll`` file in your project's folder, in the following subfolder path (once again replacing ``MyFirstPlugin`` with the name you gave your mod/project): ``MyFirstPlugin/bin/(Release or Debug)/netstandard2.1/MyFirstPlugin.dll``

Simply copy & paste this ``.dll`` file into the ``BepInEx/plugins`` folder, in your game directory, and it should run the mod. I recommend keeping the default ``LogInfo`` statement in your ``Awake`` method that comes with the template. If you have this statement, you should see it appear in the console that opens when you run the game (after installing BepInEx, and enabling the console as per the first wiki article).

### Additional guides
I highly recommend reading through the rest of the [official BepInEx guide](https://docs.bepinex.dev/articles/dev_guide/plugin_tutorial/2_plugin_start.html) for extra information.

## Next steps
I recommend reading through lethal.wiki's very short guide on [open-source & ethics](https://lethal.wiki/dev/open-source-and-ethics), to help foster a healthy modding community.

I also recommend renaming your mod's main class to ``Plugin.cs``.

Once you've finished a mod, you can [publish it](https://lethal.wiki/dev/publishing-your-mod)