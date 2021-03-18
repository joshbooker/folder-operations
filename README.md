# folder-operations

This extension demonstrates how to use a command contributed by an extension to populate a QuickPick.  That Quickpick can be used in an pickString input variable in a task or launch configuration.


## Features



\!\[Demo of task listing files in a selected folder from all folders in a workspace\]\(images\commandPickTest.gif\)

## Extension Commands

`folder-operations.getFoldersInWorkspace` : get all folders in the current workSpace and return them as an array of strings in a `QuickPick`.

## Extension Settings

This extension contributes no settings.

## Release Notes

### 0.5.0  Initial release.

## Setup


1. [Prepare to Publish Extensions](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)
1. [Package Extension](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#packaging-extensions)
1. install vsix ``` code --install-extension my-extension-0.0.1.vsix ```

## Usage : git init example

1. [create gitinit.cmd](https://gist.github.com/joshbooker/b34b172fcbb0995336b69a3424b39ab1#file-gitinit-cmd)
1. edit user tasks to call extension
    * ``` ctrl + shift + P ```
    * type ``` tasks  ```
    * select ``` Open User Tasks ```  
    * paste in [tasks.json](https://gist.github.com/joshbooker/b34b172fcbb0995336b69a3424b39ab1#file-tasks-json)

    <script src="https://gist.github.com/joshbooker/b34b172fcbb0995336b69a3424b39ab1.js"></script>
