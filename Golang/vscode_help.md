### VSCode Golang代码提示

1. 首先，需要安装好 go 插件，之间在插件市场输入go，选一个即可安装。

2. 然后，需要安装 go 的工具包。在 vscode 中，输入快捷键：command(ctrl) + shift + p，在弹出的窗口中，输入：go:install/Update Tools，回车后，选择所有插件(勾一下全选)，点击确认，进行安装（最好翻墙安装）。

3. 接下来，在项目的 settings.json 文件中添加配置：
    ```
    "go.autocompleteUnimportedPackages": true,
    "go.docsTool": "gogetdoc",
    "go.formatTool": "goimports",
    ```
4. 重启 VSCode。