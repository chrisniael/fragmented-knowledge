# Windows Terminal

配置文件路径：`%localappdata%\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\profiles.json`

## 主题

https://github.com/mbadolato/iTerm2-Color-Schemes/tree/master/windowsterminal

```json
{
    "profiles": [
        {
            "guid": "{2c4de342-38b7-51cf-b940-2309a097f518}",
            "hidden": false,
            "name": "Ubuntu",
            "source": "Windows.Terminal.Wsl",
            "colorScheme": "Gruvbox Dark"
        }
    ],

    "schemes": [
        {
            "name": "Gruvbox Dark",
            "black": "#1e1e1e",
            "red": "#be0f17",
            "green": "#868715",
            "yellow": "#cc881a",
            "blue": "#377375",
            "purple": "#a04b73",
            "cyan": "#578e57",
            "white": "#978771",
            "brightBlack": "#7f7061",
            "brightRed": "#f73028",
            "brightGreen": "#aab01e",
            "brightYellow": "#f7b125",
            "brightBlue": "#719586",
            "brightPurple": "#c77089",
            "brightCyan": "#7db669",
            "brightWhite": "#e6d4a3",
            "background": "#1e1e1e",
            "foreground": "#e6d4a3"
        }
    ]
}
```

## 字体 

https://github.com/be5invis/Sarasa-Gothic/releases


```json
{
    "profiles": [
        {
            "guid": "{2c4de342-38b7-51cf-b940-2309a097f518}",
            "hidden": false,
            "name": "Ubuntu",
            "source": "Windows.Terminal.Wsl",
            "fontFace" : "等距更纱黑体 T SC",
            "fontSize" : 12
        }
    ]
}
```


## GUID

可以手动生成 GUID，打开 PowerShell，执行

```bat
[guid]::NewGuid()
```

## 默认 Profile

```json
{
    "defaultProfile": "{2c4de342-38b7-51cf-b940-2309a097f518}"
}
```

`defaultProfile` 的值是相应 profile 的 `{guid}`。


## 官方文档

* https://github.com/microsoft/terminal/blob/master/doc/user-docs/UsingJsonSettings.md
* https://github.com/microsoft/terminal/blob/master/doc/cascadia/SettingsSchema.md
