# ContentLib

ContentLib is an API that (currently) allows for the addition of custom monsters and content events to the game.
Plans for the future also include custom items, maps, cosmetics, and sponsors.

## Requirements
To begin with ContentLib development, you will need the following mods:

* [BepInExPack by BepInEx](https://thunderstore.io/c/lethal-company/p/BepInEx/BepInExPack/)
* [ContentLib by Novinity](https://thunderstore.io/c/content-warning/p/Novinity/ContentLib/)

These can be installed with a mod manager such as r2modman or Thunderstore manager, or installed manually.

## Development Environment
You will need to start by creating a plugin (see [Starting A Mod](Starting-A-Mod.md)) and adding the ContentLib DLL as a project reference. This can be done as follows:
#### Visual Studio {collapsible="true"}
> Right click your project in the Solution Explorer
> 
> ![RightClickProject.png](RightClickProject.png)
> 
> From the list go to Add > Project Reference
> 
> ![AddReference.png](AddReference.png)
> 
> In the window that pops up, select "Browse"
> 
> ![BrowseRef.png](BrowseRef.png)
> 
> Locate the mod DLL in your mods folder and click "Add"
> 
> ![CLDLL.png](CLDLL.png)
> 
> Finally, click OK
> 
> ![ClickOK.png](ClickOK.png)
{style="tip"}

#### Rider {collapsible="true"}
> Right click your project in the explorer
> 
> ![RiderRightClickProject.png](RiderRightClickProject.png)
> 
> From the list go to Add > Reference...
> 
> ![RiderAddReference.png](RiderAddReference.png)
> 
> In the window that pops up, click "Add From..."
> 
> ![RiderAddFrom.png](RiderAddFrom.png)
> 
> Locate the mod DLL in your mods folder and click "Open"
> 
> ![OpenFileRider.png](OpenFileRider.png)
{style="tip"}

#### Visual Studio Code {collapsible="true"}
> Open the .csproj file
> 
> ![VSCodeOpenProj.png](VSCodeOpenProj.png)
> 
> In the shown area,
> 
> ![VSCodeSpace.png](VSCodeSpace.png)
> 
> place the following code, replacing "path\to\your\dll" with the directory path to the ContentLib DLL.
> ```XML
> <ItemGroup>
>   <Reference Include="ContentLib">
>       <HintPath>path\to\your\dll</HintPath>
>   </Reference>
> </ItemGroup>
> ```
> 
> Example:
>
> ```XML
> <ItemGroup>
>   <Reference Include="ContentLib">
>       <HintPath>F:\AppData\Roaming\r2modmanPlus-local\ContentWarning\profiles\Dev\BepInEx\plugins\ContentLib.dll</HintPath>
>   </Reference>
> </ItemGroup>
> ```
> 
> Save, and you're done!
{style="tip"}

#### .
You'll also want to add the ContentLib mod ID as a BepInEx dependency, which can be done by adding a BepInDependency attribute, like so:
```C#
[BepInPlugin(MyPluginInfo.PLUGIN_GUID, MyPluginInfo.PLUGIN_NAME, MyPluginInfo.PLUGIN_VERSION)]
[ContentWarningPlugin(MyPluginInfo.PLUGIN_GUID, MyPluginInfo.PLUGIN_VERSION, false)]
[BepInDependency(ContentLib.Plugin.ModGUID)]
public class MyPlugin : BaseUnityPlugin
```

This is also a quick way of ensuring you've correctly added the ContentLib as a package reference, as otherwise this will give you an error.

## Content Warning Unity project
In order to make mods for ContentLib, you will almost certainly need to use a decompiled Content Warning Unity project so you can access the game scripts. For this you should use _.

## Specific tutorials
Each page below goes through the full process of creating a mod for the given part of Content Warning via ContentLib. These will use the template project above as a base.

* [Custom Monsters](Custom-Monsters.md)