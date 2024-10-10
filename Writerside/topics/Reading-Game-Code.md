# Reading Game Code

> **INFO**
>
> This tutorial is taken and adapted from the [Lethal Company Modding Wiki](https://lethal.wiki). For more resources refer to that.
>

## Introduction
Chances are, early on in your modding journey you will be met by quite a conundrum - You want to know how something in the game works, but there is an issue! You cannot just open the game's files to find it.

You see, the way Unity games work, is that their code gets compiled into a .dll file, which you cannot normally open.

## Decompilers
Fortunately, there is something called a "decompiler". What it does, is it grabs the game's code and reverses the process, resulting in readable code. While it is not perfect, it gets it's job done.

Currently there are 3 decompilers that are widely used:

[dnSpyEx](https://github.com/dnSpyEx/dnSpy), [ILSpy](https://github.com/icsharpcode/ILSpy) and [dotPeek](https://www.jetbrains.com/decompiler/).

> **INFO**
> 
> Picking which decompiler to use is up to personal preference, but for this article ILSpy will be used due to it's balance between simplicity and power.
> 

> **DANGER**
> 
> Please keep in mind that while decompiling and reading the code is not illegal, distributing said decompiled code is illegal. Same applies for sharing the game's files.
>
> What this means is that you CANNOT bundle any of the game's files with your mods.
> 
{style="warning"}

## Opening the game DLL
Upon starting ILSpy you will be met with a window similar to this

![ILSpy Window](ilspy-window.png)

From then you want to open the ``Assembly-CSharp.dll`` file present in the game's files.

To get it you need to do the following:

### 1. Open game files. On Steam it's done as simple as right-clicking the game and pressing 'Browse local files'.

![Browse Local Files](cwbrowselocalfiles.png)

The game files folder will open

![Game Files Folder](cwgamefiles.png)

### 2. Go to ``Content Warning_Data/Managed``
Once you do that you will see many .dll files.

![Many DLLS](cwmanagedfolder.png)

Copy the path and go back to ILSpy.

### 3. Open the file in ILSpy
In ILSpy click on ``File -> Open``.

![FileOpen](ilspy-open.png)

In an opened file browser paste the path you copied earlier for easy access, select ``Assembly-CSharp.dll``, and press 'Open'.

![SelectAssembly](ilspy-opendialog.png)

After you have opened the file you should see that it has been added to the sidebar.

![ImportedFile](ilspy-imported.png)

## Reading the game code
Click on the little ``+`` left of the file name. You should see a bunch of things pop up in a list.

![ILSpy Expanded](ilspy-expanded.png)

Those are called [namespaces](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/namespaces) and are basically just used to organize code into groups. Nearly all of the game's code is stored under the ``{}`` (blank) namespace, so open that by clicking on the ``+`` again.

You will see a list of files, all containing code used by the game. If you double click any of them you can see the code inside.

![ILSpy Namespace Expanded](ilspy-namepsaceexpanded.png)

## Searching fields and methods
Obviously, with so many different files it may be difficult to find out a specific function you need. Luckily, ILSpy has a solution - Search tool.

To open the search tool you can either:

Open it by clicking on ``Window -> Search``.

![ILSpy Search](window-search.png)

OR

By clicking on the little magnifying glass icon on the topbar.

![ILSpy Search 2](glass-icon.png)

Either way the Search window will open.

![ILSpy Search Window](ilspy-searchwindow.png)

Using it is quite simple. You can type something in the search bar, and it will be displayed:

![ILSpy Search Window 2](ilspy-searchwindow2.png)

If you want to limit the search to only variables(fields) you can select so in the dropdown next to the search bar:

![ILSpy Search Window 3](ilspy-searchwindow3.png)

## Finding usage
A lot of the times, once you find something you need, you may want to know where it's being used. There is a tool for that as well.

By right-clicking on any field or method, in a context menu you can select "Analyze".

![ILSpy Analyze](ilspy-analyze.png)

After clicking on it a small window with several dropdowns will open.

![ILSpy Analyze Window](ilspy-analyzewindow1.png)

Here is what most used dropdowns stand for in fields and methods:


### Fields

``Read By`` - Methods which use this field inside of them.

![ILSpy Analyze Window 2](ilspy-analyzewindow2.png)

``Assigned By`` - Methods which assign value to this field.

![ILSpy Analyze Window 3](ilspy-analyzewindow3.png)

### Methods

``Uses`` - List of fields and methods that this method is using.

![ILSpy Analyze Window 4](ilspy-analyzewindow4.png)

``Used By`` - Methods which use this method.

![ILSpy Analyze Window 5](ilspy-analyzewindow5.png)

## Conclusion

Congrats! Now you know how to read game's code and how to find something that you need. Remember that if you cannot find something - There is no shame in asking. So, in case you need any help, you can get some in the [Content Warning Modding Discord](https://discord.gg/xyZZBQRu5S).