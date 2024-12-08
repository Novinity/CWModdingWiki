# Registering the Monster

So you've managed to make a monster in Unity and code its AI. Great! Now time to actually add it into the game.

First thing's first, place your exported asset bundle into the folder where your exported mod will go, ensure they are in the same directory.

Now, open up your main ``Plugin.cs`` file in your chosen code editor.
The first thing we need to do in our code is unpack the asset bundle.
ContentLib makes this easy, simply call the ``LoadAssetBundle`` method from the mod's ``BundleHelper``, as follows:
```C#
public static AssetBundle MyAssetBundle;
private void Awake() {
    ...
    MyAssetBundle = ContentLib.Modules.BundleHelper.LoadAssetBundle("your asset bundle name");
}
```

Next you want to load your monster object from your asset bundle. Make sure you remember the name of the prefab!
```C#
private void Awake() {
    ...
    GameObject MyMonsterObject = MyAssetBundle.LoadAsset<GameObject>("MonsterObject.prefab");
}
```

Finally, you want to register the monster and its content event with ContentLib:
```C#
private void Awake() {
    ...
    ContentLib.Modules.Monsters.CustomMonster monster = ContentLib.Modules.Monsters.RegisterMonster(new ContentLib.Modules.Monsters.CustomMonster(MyMonsterObject, 100));
    ContentLib.Modules.ContentHandler.RegisterEvent(new MyMonstersContentEvent());
}
```

Altogether, it should look similar to this:
```C#
public static AssetBundle MyAssetBundle;
private void Awake() {
    MyAssetBundle = ContentLib.Modules.BundleHelper.LoadAssetBundle("your asset bundle name");
    GameObject MyMonsterObject = MyAssetBundle.LoadAsset<GameObject>("MonsterObject.prefab");
    ContentLib.Modules.Monsters.CustomMonster monster = ContentLib.Modules.Monsters.RegisterMonster(new ContentLib.Modules.Monsters.CustomMonster(MyMonsterObject, 100));
    ContentLib.Modules.ContentHandler.RegisterEvent(new MyMonstersContentEvent());
}
```

And that's it! Start the game and your monster should be spawning, assuming there are no issues with its other code or prefab.

Alternatively, you can quickly register all monsters in a bundle with one line. This is quicker, but allows for less customization.
```C#
public static AssetBundle MyAssetBundle;
private void Awake() {
    ...
    MyAssetBundle = ContentLib.Modules.BundleHelper.LoadAssetBundle("your asset bundle name");
    ContentLib.Modules.Monsters.RegisterAllInBundle(MyAssetBundle);
}
```