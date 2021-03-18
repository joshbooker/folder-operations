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

# Setup


1. [Prepare to Publish Extensions](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)
1. [Package Extension](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#packaging-extensions)
1. install vsix: ``` code --install-extension my-extension-0.0.1.vsix ```

# Usage : git init example

1. create a [GitHub Personal Access Token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
1. create a ``` token.secret ``` file containing the token and user.  Make sure to ignore this file in your source control
    ```
    Token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    User=GitHubUserName
    ```
1. create [gitinit.cmd](https://gist.github.com/joshbooker/b34b172fcbb0995336b69a3424b39ab1#file-gitinit-cmd)
    ```
    @echo off
    for /f "delims== tokens=1,2" %%G in (token.secret) do set %%G=%%H
    cd %1
    git init
    echo "README" > README.md   
    (echo /bin && echo /obj && echo *.log && echo *.dacpac && echo *.bacpac && echo !/refs/*.dacpac && echo *.secret) > .gitignore
    git add .
    echo "Authorization: token %Token%"

    curl -X POST -i -H "Authorization: token %Token%" https://api.github.com/user/repos -d "{\"name\": \"%1\"}"
    git commit -m "first commit"

    git remote add origin https://github.com/%User%/%1.git
    git branch -M main
    git push -u origin main
    ```
1. edit vscode user tasks to call your extension
    * ``` ctrl + shift + P ```
    * type ``` tasks  ```
    * select ``` Open User Tasks ```  
    * paste in [tasks.json](https://gist.github.com/joshbooker/b34b172fcbb0995336b69a3424b39ab1#file-tasks-json)
    ```
    {
        // See https://go.microsoft.com/fwlink/?LinkId=733558
        // for the documentation about the tasks.json format
            "version": "2.0.0",
            "tasks": [
        
            {
                "label": "Git Init Project Directory",
                "type": "shell",
                "command": "gitinit.cmd ${input:pickTestDemo}",            // your command here
                "args": [
                "${input:pickTestDemo}"  // wait for the input by "id" below
                ],
                "problemMatcher": []
            }
            ],
            "inputs": [
            {
                "id": "pickTestDemo",
                "type": "command",
                "command": "folder-operations.getFoldersInWorkspace"  // returns a QuickPick element
            },
            ]
    }
    ```