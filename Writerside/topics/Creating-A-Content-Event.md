# Creating A Content Event

Creating a content event for your monster is simple as it's done the same way the base game does it.

```C#
public class MyMonstersContentEvent : MonsterContentEvent {
    public static string[] NORMAL_COMMENTS = new string[3]
  {
    "Comment 1!",
    "Comment 2!",
    "Comment 3!"
  };

    public override Comment GenerateComment() {
        return new Comment(NORMAL_COMMENTS.GetRandom());
    }

    public override float GetContentValue() {
        return 60f;
    }

    public override ushort GetID() {
        return ContentLib.Modules.ContentHandler.GetEventID(GetType().Name);
    }

    public override string GetName() => "My Monster";
}
```

The ``NORMAL_COMMENTS`` variable lists all possible comments that can be received when your monster is on screen.

Change the return value of ``GetContentValue`` to change how many views a comment on your monster gives.

Change the return value of ``GetName`` to then name of your monster.

You can then add this as a component to your monster in Unity.