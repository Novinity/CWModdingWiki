# Logging

> **INFO**
>
> This tutorial is taken and adapted from the [Lethal Company Modding Wiki](https://lethal.wiki). For more resources refer to that.
>

Logging is a very useful debugging tool for developers. You can look at the console or the log file to see if everything ran correctly, or if errors occurred.

Where you have to be careful though is the fact that writing to the console can create game lag/stuttering due to how the console works. This article goes through the best practices in utilizing the Logger.

## Logger Setup
When using BepInEx, you may notice that it typically comes with the following ``Awake`` method:
```C#
private void Awake() {
    // Plugin startup logic
    Logger.LogInfo($"{MyPluginInfo.PLUGIN_GUID} v{MyPluginInfo.PLUGIN_VERSION} has loaded!");
}
```

The third line uses the Logger to log to the console and log file that your plugin had loaded. In the console, it may look like the following:

![Example Bepinex Log](examplebepinexlog.png)

Currently the Logger is an ``internal`` variable, which is what we want. The ``internal`` access modifier allows only our project code to access the field. It is also ``static`` to allow our other classes to easily access the logger by doing ``Plugin.Logger``. The ``new`` keyword lets the compiler know that we are creating a new instance of the Logger.

After that we see ``{ get; private set; }``, which means that other classes are allowed to ``get`` the Logger, but never ``set`` it. Then we initialize it to ``null!``, which means we are setting a non-nullable type to null anyway.

```C#
internal new static ManualLogSource Logger { get; private set; } = null!;
```

Next we set that field to the Logger given by BepInEx. Since we are overriding it, we use base.Logger to reference Logger from the BaseUnityClass we inherit from.
```C#
private void Awake() {
    Logger = base.Logger;
    
    ...
    
    Logger.LogInfo($"{MyPluginInfo.PLUGIN_GUID} v{MyPluginInfo.PLUGIN_VERSION} has loaded!");
}
```

Now that we've explained that, it's time to get to logging!

## Using the Logger
Ensure you have ``[HarmonyPatch]`` at the top of any class you are putting a patch in:
```C#
[HarmonyPatch]
public class Plugin : BaseUnityPlugin {
    ...
}
```

So, you have a patch and want to log info to the console during it. For example, we want to log the item name when an item is picked up. We can patch the ``Pickup.Interact`` method, and then get the item's name:
```C#
[HarmonyPostfix]
[HarmonyPatch(typeof(Pickup), nameof(Pickup.Interact))]
private static void InteractPostfix(Player player, Pickup __instance) {
    var itemName = __instance.itemInstance.item.name;
}
```
Now we can log it! To do so, we just add one line:
```C#
[HarmonyPostfix]
[HarmonyPatch(typeof(Pickup), nameof(Pickup.Interact))]
private static void InteractPostfix(Player player, Pickup __instance) {
    var itemName = __instance.itemInstance.item.name;
    Plugin.Logger.LogDebug(itemName); // new
}
```
Notice how we use ``.LogDebug()`` here instead of ``.LogInfo()``. This is where best practices come into play.

## Best Practices

## Debug Logging

ecause logging to the console can cause the game to stutter, we'd like to avoid doing so whenever possible. However, we still would like to know what we log!

We can do so by using ``.LogDebug()``. This will log to the console, but with a lower "priority" so that it is only visible if we specify so in our BepInEx config.

To view debug logs, you can change the following in your BepInEx config located at ``BepInEx/config/BepInEx.cfg``:

```yaml
  [Logging.Console]

  #...

  ## Which log levels to show in the console output.
  # Setting type: LogLevel
  # Default value: Fatal, Error, Warning, Message, Info
  # Acceptable values: None, Fatal, Error, Warning, Message, Info, Debug, All
  # Multiple values can be set at the same time by separating them with , (e.g. Debug, Warning)
  LogLevels = All # Make sure this is All

  [Logging.Disk]

  #...

  ## Which log levels are saved to the disk log output.
  # Setting type: LogLevel
  # Default value: Fatal, Error, Warning, Message, Info
  # Acceptable values: None, Fatal, Error, Warning, Message, Info, Debug, All
  # Multiple values can be set at the same time by separating them with , (e.g. Debug, Warning)
  LogLevels = All # Make sure this is All
```

By default, if a player uses the BepInEx version pinned on Thunderstore, the ``[Logging.Disk]`` ``LogLevels`` setting will automatically be set to ``All``, more easily allowing you to debug based off "hidden" logs in the log file.

## Warning Logging
Sometimes you may have code that may not be used as intended, but will still function normally. To let users know this has occured, you can use ``.LogWarning()``.

You may commonly see warnings logged by Unity when the Voice Chat server is initializing, and this is a case where something isn't working right, but it can still continue functioning.

## Error Logging
Sometimes you need to log errors so that you can easily find it when someone runs into an issue and posts a log file. You can use ``.LogError()`` to do so.

> **WARNING**
> 
> ``LogError()`` should only be used when an error occurs.
> 
{style="warning"}

Often times, there will be C# or Unity errors that display when an error occurs, limiting the need to use the method. But it can still be a useful piece of information when debugging.