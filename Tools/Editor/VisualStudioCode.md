# `Visual Studio Code`

`Visual Studio Code`是`Microsoft`推出的一款轻量级跨平台源代码编辑器。

## Command Line Interface (CLI)

`VSCode`提供了强大的命令行工具，用于打开`VSCode`，管理`Extensions`，更改显示语言以及输出诊断信息等。

### 打开文件或文件夹

|参数|说明|
|---|---|
|`file`|打开对应名称的文件。如果文件不存在，则将创建文件并标记为已编辑状态。通过空格符分隔文件名，可以同时打开多个文件。|
|`folder`|打开对应名称的文件夹。同时打开多个文件夹，将创建一个多目录工作区。|

### 管理`Extensions`

|参数|说明|
|---|---|
|`--install-extension <ext>`|安装扩展程序。需要提供完整的扩展程序名`publisher.extension`作为参数。|
|`--uninstall-extension <ext>`|卸载扩展程序。需要提供完整的扩展程序名`publisher.extension`作为参数。|
|`--disable-extensions`|禁用所有扩展程序。已安装的扩展程序仍将在`Extensions`页面出现。|
|`--list-extensions`|列出所有已安装的扩展程序。|

## Settings

`VSCode`的配置文件`settings.json`有两种：用户配置文件和工作区配置文件。

用户配置文件根据平台不同分别存放在：

* **Windows** `%APPDATA%\Code\User\settings.json`
* **macOS** `$HOME/Library/Application Support/Code/User/settings.json`
* **Linux** `$HOME/.config/Code/User/settings.json`

工作区配置文件则存放在工作区目录下的`.vscode`文件夹中。工作区配置文件中的配置将会覆盖用户配置文件中的配置。

## Extensions