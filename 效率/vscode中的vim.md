SCodeVIM 是 VSCode 的 vim 扩展，其输入法相关的设置目仅在 macOS 和 Win 平台上支持较好，Linux 系统还有待完善。
## 解决烦人的拼音切换问题
在insert模式下如果是中文输入法，切换到normal模式默认还是中文输入，所以移动jk 会出现拼音提示，需要手动切换才能消除。
好在vscode vim 官方给出了解决方案，可以自动完成切换过程。

1. 下载：https://github.com/daipeihust/im-select
2. 修改配置。 在settings.json中配置：
   ```json
    "vim.autoSwitchInputMethod.enable": true,
    "vim.autoSwitchInputMethod.defaultIM": "com.apple.keylayout.ABC",
    "vim.autoSwitchInputMethod.obtainIMCmd": "/usr/local/bin/im-select",
    "vim.autoSwitchInputMethod.switchIMCmd": "/usr/local/bin/im-select {im}"
   ```