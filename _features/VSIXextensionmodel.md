---
title: Debugging the VSIX extension
component: common
---

## Resetting the Experimental instance (so that changes to the vsct file are detected)
The command file for a VSIX extension gets cached by Visual Studio. To flush the cache you either have to increment the version number of the add-in or run the following command 

`devenv /rootsuffix Exp /updateconfiguration`

For Visual Studio 2012 you would run this command from `C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE`  (if you did not have devenv.exe in your Path.

## Debugging an Extension
Under the "Debug" project setting set the start external program setting to the version of Visual Studio that you wish to debug.

For Visual Studio 2012 this would be something like:
`C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\devenv.exe`

in the Command Line Arguments section add `/rootSuffix Exp`

![](VSIX extension model_debugSettings.png)

### If you are debugging the same version of Visual Studio that you are compiling with
Under project properties make sure that the following are ticked:
* **TRUE** Create VSIX Container during build
* **TRUE** Deploy VSIX content to experimental instance for debugging
* **FALSE** Copy VSIX content to the following location

![](VSIX extension model_SameVersionDebug.png)

### If you are NOT debugging the same version of Visual Studio that you are compiling with
Under project properties make sure that the following are ticked:
* **TRUE** Create VSIX Container during build
* **FALSE** Deploy VSIX content to experimental instance for debugging
* **TRUE** Copy VSIX content to the following location `C:\Users\<user>\AppData\Local\Microsoft\VisualStudio\<version>\Extensions\BidsHelperExp`

Where <user> is your login and <version> is the target  instance of Visual Studio (for the VS 2012 experimental instance this would be "11.0Exp" )

![](VSIX extension model_DifferentVersionDebug.png)

## To find the ID of a menu item 
from [http://stackoverflow.com/questions/31759396/vsix-adding-a-menu-item-to-the-visual-studio-editor-context-menu](http://stackoverflow.com/questions/31759396/vsix-adding-a-menu-item-to-the-visual-studio-editor-context-menu)
* in RegEdit go to `HKEY_CURRENT_USER\SOFTWARE\Microsoft\VisualStudio\14.0\General` and set  `EnableVSIPLogging` value of `1` to enable logging.
* then navigated into the editor and with the mouse on an empty area press CTRL-SHIFT and then right click the mouse
* note that the ID is in decimal notation and will need to be converted to hex to go into the vsct file

## Code Changes for the VSIX version

The following code changes were made to each *Plugin class in order to work with the new Visual Studio extension framework

* Delete "using Extensibility;"
* Add "using BIDSHelper.Core;"
* Update constructor parameters to look like 
``` c#
    public AggregationManagerPlugin(BIDSHelperPackage package)
        : base(package)
```
instead of:
``` c#
    public AggregationManagerPlugin(Connect con, DTE2 appObject, AddIn addinInstance)
        : base(con, appObject, addinInstance)
```

* Add a call to CreateContextMenu() if adding a menu triggered command
* Delete or comment out Bitmap property (button icons are specified in the BIDSHelperPackage.vsct file)
* Delete or comment out MenuName property (menus are specified in the BIDSHelperPackage.vsct file)
* Delete or comment out ShouldPositionAtEnd property (button positions are specified by setting the group for the button in the BIDSHelperPackage.vsct file)
* add a command id and menu option to the BidsHelper.vsct file if adding a menu triggered command

