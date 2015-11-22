# `android-dumpsys-filters`

This repository contains scripts that filter the output from various Android `dumpsys` commands to make them more readable.

## The Activity Manager

You can view all the activities in the system with the following command:

```
adb shell dumpsys activity
```

This command dumps a _lot_ of information.  Often, you only really care about the activity data structures, and you can focus the Activity Managers output with the `[a]ctivities` argument:

```
adb shell dumpsys activity activities
```

Even this produces quite a lot of information, and in a format that's difficult to read.

The `filter-tasks` shell script parses the output of that latter command and rearranges it to show activities in a more readable way. For example:

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
