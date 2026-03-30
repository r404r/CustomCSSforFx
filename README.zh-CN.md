## 语言版本

- [English](README.md)
- [简体中文](README.zh-CN.md)
- [日本語](README.ja.md)

## 预览

默认状态：  
![默认预览](assets/preview-001.png)

鼠标悬停在工具栏上：  
![工具栏悬停预览](assets/preview-002.png)

## Firefox 下载

- **[CustomCSSforFx - 当前版本与更新日志](https://github.com/Aris-t2/CustomCSSforFx/releases)** - **[最后一个支持 102 ESR 的版本](https://github.com/Aris-t2/CustomCSSforFx/releases/tag/4.2.8)**  
- **[Firefox 自定义 JavaScript 脚本](https://github.com/Aris-t2/CustomJSforFx)** - **[NoiaButtons CSS 微调](https://github.com/Aris-t2/NoiaButtons)**  


## 许可证

本项目采用 GPLv3 和 MPL 2.0 双许可证，具体条款请参阅 LICENSE 文件。  


## 说明 / 使用方法 / README

- [启用自定义 CSS](#unlock-custom-css-usage)
- [为什么 WebExtensions 无法正确修改 Firefox 外观](#webextensions-can-not-modify-firefox-appearance-properly)
- [Firefox 配置文件夹在哪里？用户样式的正确放置位置](#where-to-find-firefox-profile-folder-the-correct-location-for-user-styles)  
- [如何使用自定义用户样式？](#how-to-use-custom-user-styles)  
- [如何查找元素 id 和属性？](#how-to-find-item-ids-and-attributes)  
- [自定义 CSS 代码应该放在哪里？](#where-to-add-custom-css-code)
- [如何修改自定义用户样式？](#how-to-modify-custom-user-styles)  
- [Firefox Color（与 CustomCSSforFx 默认配色预设兼容）](https://color.firefox.com/)    

<a id="unlock-custom-css-usage"></a>
## 启用自定义 CSS

`about:config` > `toolkit.legacyUserProfileCustomizations.stylesheets` > `true`  

<a id="webextensions-can-not-modify-firefox-appearance-properly"></a>
## 为什么 WebExtensions 无法正确修改 Firefox 外观

想要修改 Firefox 界面，目前唯一可行的方式，是把自定义 CSS 写入浏览器配置文件夹中的 **userChrome.css** 和 **userContent.css**。  
也请注意，CSS 不能凭空创建全新的项目、按钮或工具栏，它只能调整 Firefox 已经存在的界面元素。  

<a id="where-to-find-firefox-profile-folder-the-correct-location-for-user-styles"></a>
## Firefox 配置文件夹在哪里？用户样式的正确放置位置

**1.** 找到你的配置文件夹（每个人的配置文件名称都不同）。  
`about:support > 配置文件夹 > 打开文件夹`  
或 `about:profiles > 根目录 > 打开文件夹`  

**2.** 用户样式应放在 `\chrome\` 文件夹中。如果还没有这个文件夹，请手动创建。完成后目录结构应如下所示：  
`\ PROFILE FOLDER NAME \chrome\`  

**3.** 将 `userChrome.css`、`userContent.css` 以及 `\config\`、`\css\`、`\image\` 文件夹复制到 `\chrome\` 文件夹中。完成后目录结构应如下所示：  
`\chrome\config\`  
`\chrome\css\`  
`\chrome\image\`  
`\chrome\userChrome.css`  
`\chrome\userContent.css`  

（可选）磁盘中的配置文件夹位置：  
**Windows**  
`C:\Users\ USERNAME \AppData\Roaming\Mozilla\Firefox\Profiles\ PROFILE FOLDER NAME \`  
若要看到 `AppData` 文件夹，需要启用显示隐藏文件。也可以直接在资源管理器地址栏输入 `%APPDATA%\Mozilla\Firefox\Profiles\`。  
**Linux**  
`/home/ username /.mozilla/firefox/ profile folder name /`  
若要看到 `.mozilla` 文件夹，需要启用显示隐藏文件。  
**Mac OS X**  
`~\Library\Mozilla\Firefox\Profiles\ PROFILE FOLDER NAME \` 或  
`~\Library\Application Support\Mozilla\Firefox\Profiles\ PROFILE FOLDER NAME \`  
`\Users\ USERNAME \Library\Application\Support\Firefox\Profiles\`  

<a id="how-to-use-custom-user-styles"></a>
## 如何使用自定义用户样式？

_userChrome.css_ 和 _userContent.css_ 更像是选项 / 配置文件，主要功能都可以在这里启用或禁用。  
使用任意文本编辑器编辑 _userChrome.css_ 和 _userContent.css_（Windows 推荐使用 **[Notepad++](https://notepad-plus-plus.org/download/)**），通过修改、删除或注释已有的 `@import` 语句，即可开启或关闭你想要的功能。  
每次修改后都需要重启 Firefox，改动才会生效。  

**示例**  
如果想要<u>启用</u>“导航工具栏按钮的经典外观”，对应这一行应写成：  
`@import "./css/buttons/buttons_on_navbar_classic_appearance.css"; /**/`  

如果想要<u>禁用</u>“导航工具栏按钮的经典外观”，对应这一行应写成：  
`/* @import "./css/buttons/buttons_on_navbar_classic_appearance.css"; /**/`  

注意  
位于 `/*` 和 `*/` 之间的代码不会被 Firefox 使用，除非中间又出现了其他 `/*` 或 `*/`。  

<a id="how-to-find-item-ids-and-attributes"></a>
## 如何查找元素 id 和属性？

只需启用一次：  
1\. 工具 > Web 开发者 > 切换工具 > “自定义工具和获取帮助”按钮（即三点按钮）> 设置 > 启用浏览器界面和附加组件调试工具箱  
2\. 工具 > Web 开发者 > 切换工具 > “自定义工具和获取帮助”按钮（即三点按钮）> 设置 > 启用远程调试  

或者在 about:config 中把以下两个选项设为 true：  

about:config > devtools.chrome.enabled > true  
about:config > devtools.debugger.remote-enabled > true  

按下 `Ctrl+Alt+Shift+I`，或者打开“工具 > Web 开发者 > 浏览器工具箱”。  

随后即可检查界面元素或网页内容。  

如果想在检查时强制保持弹出菜单不自动关闭：  
点击“自定义工具和获取帮助”按钮（即三点按钮），然后选择“禁用弹出窗口自动隐藏”。  

<a id="where-to-add-custom-css-code"></a>
## 自定义 CSS 代码应该放在哪里？

`userChrome.css` 在末尾导入了 `my_userChrome.css` 文件（如果存在）。这是专为你自己的 CSS 代码预留的位置。

| 修改类型 | 修改位置 |
|---------|---------|
| 启用/禁用已有功能模块 | `userChrome.css`（切换 `@import` 注释） |
| 调整已有模块的变量值（颜色、尺寸等） | 对应的 `config/*.css` 文件 |
| 项目没有提供的新自定义样式 | `my_userChrome.css` |
| 修复已有模块的 bug | 视情况：小修放 `my_userChrome.css`，大改直接改模块文件 |

`my_userChrome.css` 在 `userChrome.css` 的最后被导入，加载优先级最高，可以覆盖上方所有模块的样式。更重要的是，升级上游项目时 `my_userChrome.css` 不会被覆盖。

<a id="how-to-modify-custom-user-styles"></a>
## 如何修改自定义用户样式？

使用文本编辑器打开 CSS 文件，查看代码后按你的需要调整数值。  
有些文件还包含额外说明，用于指导你针对特定场景微调界面。  
修改后请重启 Firefox，使改动生效。  

_示例_  
打开 `./css/tabs/classic_squared_tabs.css` 文件  
查找 `/* unloaded/pending tabs color *//*`  
删除行尾的 `/*`，让这部分代码生效。保存文件后重启 Firefox。  

_示例 2_  
打开 `userChrome.css` 文件  
查找 `@import "./css/tabs/classic_squared_tabs.css"; /**/`  
在行首加上 `/*`，即可禁用 “classic squared tabs” 外观。  
结果应如下所示：`/* @import "./css/tabs/classic_squared_tabs.css"; /**/`  
  
_示例 3_  
打开 `userChrome.css` 文件    
查找 `/* @import "./css/locationbar/reader_alternative_icon.css"; /**/`  
删除行首的 `/*`，即可启用替代版阅读器图标外观。  
结果应如下所示：`@import "./css/locationbar/reader_alternative_icon.css"; /**/`  

## 为 `chrome` 文件夹使用符号链接

如果你经常修改 CSS，不想在每次改动后都手动把 `current/` 中的文件复制到 Firefox 配置文件中，也可以直接把配置文件里的 `chrome` 文件夹链接到仓库的 `current/` 文件夹。

在 macOS 或 Linux 上，可以通过符号链接实现。

示例：

```bash
ln -s "/path/to/CustomCSSforFx/current" "/path/to/Firefox/Profile/chrome"
```

在这种设置下，Firefox 会直接从仓库副本中读取文件。
这对频繁修改 CSS 很方便，因为你只需要重启 Firefox，而不必再次复制文件。

注意事项：

- 在创建链接前，请先删除或重命名现有的配置文件 `chrome` 文件夹
- 确保被链接的 `current/` 文件夹中包含 `userChrome.css`、`userContent.css`、`config/`、`css/` 和 `image/`
- 每次修改后都要重启 Firefox

在 Windows 上，也可以考虑使用目录符号链接或 junction，将配置文件中的 `chrome` 文件夹指向仓库的 `current/` 文件夹，但这里尚未实际测试。
