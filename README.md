# `android-dumpsys-filters`

Scripts that filter the output from some Android `dumpsys` commands to make them more readable.

<br/>
## The Activity Manager

You can view the state of the Activity Manager with the following command:

<br/>
```
adb shell dumpsys activity
```
<br/>

This command dumps a _lot_ of information.  Often, you only really care about the activity data structures, and you can focus the Activity Manager's output with the `[a]ctivities` argument:

<br/>
```
adb shell dumpsys activity activities
```
<br/>

Even this produces quite a lot of information, and in a format that's difficult to read.

The `filter-tasks` shell script parses the output of that latter command and rearranges it to show activities in a more readable way. For example:

<br/>
```
$ adb shell dumpsys activity a | filter-tasks


Activity Stack #0
─────────────────

    Task #1 (21a4a334) Affinity=com.android.launcher
    ──┬───────────────
      │ (21a496e0) com.android.launcher/com.android.launcher2.Launcher
      └───────────────

    Resumed Activity: (21a496e0) com.android.launcher/com.android.launcher2.Launcher


Activity Manager Service Metadata
─────────────────────────────────

  Focused Activity: (21a496e0) com.android.launcher/com.android.launcher2.Launcher

  Recent Tasks
  ────────────
    [0] #1 (21a4a334) Affinity=com.android.launcher
```
<br/>

<br/>
## The Window Manager

You can view the state of the Window Manager with the following command:

<br/>
```
adb shell dumpsys window
```
<br/>

This command dumps a _lot_ of information.  Often, you only really care about the window data structures, and you can focus the Window Manager's output with the `[w]indows` argument:

<br/>
```
adb shell dumpsys window windows
```
<br/>

Even this produces quite a lot of information, and in a format that's difficult to read.

The `filter-windows` shell script parses the output of that latter command and rearranges it to show windows in a more readable way. For example:

<br/>
```
$ adb shell dumpsys window w | filter-windows


Window #5 (21a6b5cc) SearchPanel
────────────────────────────────
  Owner's UID         : 10011
  Package             : com.android.systemui
  App Operation       : NONE
  Base Layer          : 211000
  View Visibility     : Invisible
  Obscured            : false
  Frames              : Content: [0,0][960,608]  Visible: [0,0][960,608]
  Flags               : 0x820100
  Private Flags       : 0x0
  System UI Visibility: 0x400


Window #4 (219ecbac) NavigationBar
──────────────────────────────────
  Owner's UID         : 10011
  Package             : com.android.systemui
  App Operation       : NONE
  Base Layer          : 201000
  View Visibility     : Visible
  Obscured            : false
  Frames              : Content: [0,560][960,608]  Visible: [0,560][960,608]
  Flags               : 0x840068
  Private Flags       : 0x0
  System UI Visibility: 0x0


Window #3 (21a14fbc) StatusBar
──────────────────────────────
  Owner's UID         : 10011
  Package             : com.android.systemui
  App Operation       : NONE
  Base Layer          : 161000
  View Visibility     : Visible
  Obscured            : false
  Frames              : Content: [0,0][960,25]  Visible: [0,0][960,25]
  Flags               : 0x1840048
  Private Flags       : 0x0
  System UI Visibility: 0x0


Window #2 (21a1f3f0) KeyguardScrim
──────────────────────────────────
  Owner's UID         : 1000 SYSTEM_UID
  Package             : android
  App Operation       : NONE
  Base Layer          : 121000
  View Visibility     : Gone
  Obscured            : false
  Frames              : Content: [0,25][960,560]  Visible: [0,25][960,560]
  Flags               : 0x110900
  Private Flags       : 0x0
  System UI Visibility: 0x3610000


Window #1 (21aa4498) com.android.launcher/com.android.launcher2.Launcher
────────────────────────────────────────────────────────────────────────
  Owner's UID         : 10012
  Package             : com.android.launcher
  App Operation       : NONE
  Base Layer          : 21000
  Activity            : (21a5d600) com.android.launcher/com.android.launcher2.Launcher
  View Visibility     : Visible
  Obscured            : false
  Frames              : Content: [0,25][960,560]  Visible: [0,25][960,560]
  Flags               : 0x1910100
  Private Flags       : 0x8
  System UI Visibility: 0x400


Window #0 (2199b388) com.android.systemui.ImageWallpaper
────────────────────────────────────────────────────────
  Owner's UID         : 10011
  Package             : null
  App Operation       : NONE
  Base Layer          : 21000
  View Visibility     : Visible
  Obscured            : false
  Frames              : Content: [0,0][1600,1280]  Visible: [0,0][1600,1280]
  Flags               : 0x318
  Private Flags       : 0x0
  System UI Visibility: 0x0


Window Manager Service Metadata
───────────────────────────────

  Focused Activity: (21a5d600) com.android.launcher/com.android.launcher2.Launcher
```
<br/>
