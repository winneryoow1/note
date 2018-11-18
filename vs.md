# vscode常用快捷键及常用设置

## 快捷键

- `ctrl+b` 切换侧边栏
- `ctrl+\` 拆分编辑器
- `ctrl+鼠标滚轮` 缩放编辑器的字体
- `alt+shift+f` 整理代码格式
- `alt+z` 切换自动换行
- `ctrl+·` 打开终端调试
- `ctrl+shift+n` 新建窗口
- `ctrl+p` 文件内搜索(聚焦在某个文件)
- `ctrl+shif+f` 全编辑器搜索(聚焦在资源管理器)
- `单击文件` 预览(再点别的会替换成其他)
- `双击文件` 编辑文件(固定在工作区)
- alt + up/down 上下移动当前行或选中区域
- alt + shift + up/down 复制当前行货选中区域到上/下行
- ctrl + b 隐藏侧边栏
- ctrl + ` 打开控制台终端
- alt + shift + f 格式化代码
- ctrl + [ / ] 向左或有缩进
- ctrl + 1 / 2/ 3 拆分编辑器
- ctrl + + / - 缩放字体
- ctrl + home/end 跳转页面顶部或尾部
- ctrl + r 显示最近打开文件
- ctrl + shift + n 打开新窗口
- ctrl + x 剪切行
- ctrl + enter 在下面插入行,无论此时光标是否在行末尾
- ctrl + shift + enter 与楼上相反
- ctrl + shift + [ / ] 折叠或展开选中区域
- ctrl + g 跳转某行
- alt + enter 全选

## 工作区设置

设置文件位置(中文版)：文件->首选项->工作区设置->setting.json 设置文件位置(中文版)：File > Preferences->setting.json

> **注意：**不要更改默认配置文件，更改的配置写在setting.json中即可，会自动覆盖默认配置

## 工作区常用设置

- 控制在多少个字符后编辑器会自动换到下一行。将其设置为 0 则将打开视区宽度换行(自动换行)。将其设置为 -1 则将强制编辑器始终不换行。`"editor.wrappingColumn": 0`
- 控制行号的可见性 `"editor.lineNumbers": true`
- 控制编辑器是否应呈现缩进参考线`"editor.renderIndentGuides": true`
- 控制是否自动保存更新后的文件。接受的值:“off”、“afterDelay”、“onFocusChange”(编辑器失去焦点)、“onWindowChange”(窗口失去焦点)。如果设置为“afterDelay”，则可在 "files.autoSaveDelay" 中配置延迟。`"files.autoSave": "off"`
- 控制资源管理器是否应该允许通过拖放移动文件和文件夹,(默认就是true，不需要专门修改)。`"explorer.enableDragAndDrop": true`
- 缩进 head 和 body 部分(默认false)。`"html.format.indentInnerHtml": false`