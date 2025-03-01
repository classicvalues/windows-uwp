---
title: PowerToys Run utility for Windows
description: A quick launcher for power users that contains some additional features without sacrificing performance.
ms.date: 05/28/2021
ms.topic: article
ms.localizationpriority: medium
no-loc: [PowerToys, Windows, File Explorer, PowerToys Run, WindowWalker]
---

# PowerToys Run utility

PowerToys Run is a quick launcher for power users that contains some additional features without sacrificing performance. It is open source and modular for additional plugins.

To use PowerToys Run, select <kbd>Alt</kbd>+<kbd>Space</kbd> and start typing! _(note that this shortcut can be changed in the settings window)_
![PowerToys Run demo opening apps](../images/pt-powerrun-demo.gif)

## Requirements

- Windows 10 version 1903 or higher
- After installing, PowerToys must be enabled and running in the background for this utility to work

## Features

PowerToys Run features include:

- Search for applications, folders, or files
- Search for running processes (previously known as [WindowWalker](https://github.com/betsegaw/windowwalker/))
- Clickable buttons with keyboard shortcuts (such as _Open as administrator_ or _Open containing folder_)
- Invoke Shell Plugin using `>` (for example, `> Shell:startup` will open the Windows startup folder)
- Do a simple calculation using calculator

## Settings

The following Run options are available in the PowerToys settings menu.

| Settings | Action |
| :--- | :--- |
| Open PowerToys Run | Define the keyboard shortcut to open/hide PowerToys Run |
| Ignore shortcuts in Fullscreen mode | When in full-screen (F11), PowerToys Run won't be engaged with the shortcut |
| Maximum number of results | Maximum number of results shown without scrolling |
| Clear the previous query on launch | When launched, previous searches will not be highlighted |

## Keyboard shortcuts

| Shortcuts | Action |
| :--- | :--- |
|<kbd>Alt</kbd>+<kbd>Space</kbd> (default) | Open or hide PowerToys Run |
|<kbd>Esc</kbd> | Hide PowerToys Run |
|<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Enter</kbd> | Open the selected application as administrator (only applicable to applications) |
|<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>E</kbd> | Open containing folder in File Explorer (only applicable to applications and files) |
|<kbd>Ctrl</kbd>+<kbd>C</kbd> | Copy path location (only applicable to folders and files) |
|<kbd>Tab</kbd> | Navigate through the search result and context menu buttons |

## Action keys

These default activation phrases will force PowerToys Run into only targeted plugins.

| Action key | Action | Example |
| :--- | :--- | :--- |
| `=` | Calculator only | `=2+2` |
| `?` | File searching only | `?road` to find `roadmap.txt` |
| `??` | Web search only | `??What is the answer to life` to search with your default browser's search engine. |
| `.` | Installed programs only | `.code` to get Visual Studio Code. See [Program parameters](#program-parameters) for options on adding parameters to a program's startup |
| `//` | URIs only | `//` to launch your default browser, or `//docs.microsoft.com` to have your default browser go to https://docs.microsoft.com. Also supports `mailto:` and `ms-settings:` |
| `<` | Running processes only | `<outlook` to find all processes that contain outlook |
| `>` | Shell command only | `>ping localhost` to do a ping query |
| `:` | Registry keys only | `:hkcu` to search for the HKEY_CURRENT_USER registry key |
| `!` | Windows services only | `!alg` to search for the Application Layer Gateway service to be started or stopped |
| `{` | Visual Studio Code previously opened workspaces, remote machines (SSH or Codespaces) and containers. This plugin is off by default. | `{powertoys` to search for workspaces that contain 'powertoys' in their paths |
| `%%` | Unit converter only | `%% 10 ft in m` to calculate the number of meters in 10 feet |
| `$` | Windows settings only | `$ Add/Remove Programs` to launch the Windows settings menu for managing installed programs. To list all settings of an area category, type `:` after the category name. `$ Device:` to view all available Device settings |

## System commands

PowerToys Run enables a set of system level actions that can be executed.

| Action command | Action | Note |
| :--- | :--- | :--- |
| `Shutdown` | Shuts down the computer | |
| `Restart` | Restarts the computer | |
| `Sign Out` | Signs current user out | |
| `Lock` | Locks the computer | |
| `Sleep` | Sleeps the computer | |
| `Hibernate` | Hibernates the computer | |
| `Empty Recycle Bin` | Empties the recycle bin | |
| `UEFI Firmware Settings` | Reboot computer into UEFI Firmware Settings | Only available on systems with UEFI firmware.<br />(Requires administrative permissions.) |

## Plugin manager

The PowerToys Run settings menu includes a plugin manager that allows you to enable/disable the various available plugins. By selecting and expanding the sections, you can customize the activation phrases used by each plugin. In addition, you can select whether a plugin appears in global results, as well as set additional plugin options where available.

## Program parameters

The PowerToys Run program plugin allows for program arguments to be added when launching an application. The program arguments must follow the expected format as defined by the program's command line interface.

For example, when launching Visual Studio Code, you can specify the folder to be opened with:

`Visual Studio Code -- C:\myFolder`

Visual Studio Code also supports a set of [command line parameters](https://code.visualstudio.com/docs/editor/command-line), which can be utilized with their corresponding arguments in PowerToys Run to, for instance, view the difference between files:

`Visual Studio Code -d C:\foo.txt C:\bar.txt` 

If the program plugin's option "Include in global result" is not selected, be sure to include the activation phrase, `.` by default, to invoke the plugin's behavior:

`.Visual Studio Code -- C:\myFolder`

## Calculator Plugin

The PowerToys Run calculator plugin supports the following operations:

| Operation |  Operator Syntax |
| - | - |
| Addition |  a + b |
| Subtraction | a - b |
| Multiplication | a * b |
| Division |  a / b |
| Modulo/Remainder | a % b |
| Exponentiation | a ^ b |
| Factorial | x ! |
| Sine | sin( x ) |
| Cosine | cos( x ) |
| Tangent | tan( x ) |
| Arc Tangent | arctan( x ) |

## Monitor Positioning

If multiple monitors are in use, PowerToys Run can be launched on the desired monitor by configuring the appropriate launch behavior in the Settings menu. Options are opening on:

- Primary monitor
- Monitor with mouse cursor
- Monitor with focused window

![PowerToys Run Monitor Selection](../images/pt-run-monitor.png)


## Windows Search settings

If the Windows Search plugin is not set to cover all drives, you will receive the following warning:

![PowerToys Run Indexer Warning](../images/pt-run-warning.png)

You can turn off the warning in the PowerToys Run plugin manager options for Windows Search, or select the warning to expand which drives are being indexed. After selecting the warning, the Windows settings "Searching Windows" options menu will open.

![Indexing Settings](../images/pt-run-indexing.png)

In this "Searching Windows" menu, you can:

- Select "Enhanced" mode to enable indexing across all of the drives on your Windows machine.
- Specify folder paths to exclude.
- Select the "Advanced Search Indexer Settings" (near the bottom of the menu options) to set advanced index settings, add or remove search locations, index encrypted files, etc.

![Advanced Indexing Settings](../images/pt-run-indexing-advanced.png)

## Known issues

For a list of all known issues and suggestions, see the [PowerToys product repo issues on GitHub](https://github.com/microsoft/PowerToys/issues?q=is%3Aopen+is%3Aissue+label%3A%22Product-PowerToys+Run%22).

## Attribution

- [Wox](https://github.com/Wox-launcher/Wox/)
- [Beta Tadele's Window Walker](https://github.com/betsegaw/windowwalker)
