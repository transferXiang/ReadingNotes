# GitBook 插件推荐
## 安装与使用
插件的使用将为读者提供更多友好的功能，下面将以 search-pro 的安装来做个简单介绍：
### 安装
* 在线安装  
在线安装是通过npm来进行的:`npm install gitbook-plugin-插件名称`
* 离线安装
需要先下载插件，然后再通过npm进行安装。
```
> git clone git@github.com:gitbook-plugins/gitbook-plugin-search-pro.git -b gh-pages
> cd ./gitbook-plugin-search-pro
> npm install
```
* gitbook 安装
虽然该方法最终还是通过npm进行安装，但该安装方式更加简单方便。仅需在book.json中定义你需要使用的插件，然后执行`gitbook install`则会自动的进行安装  
有的时候通过`gitbook install`进行安装时较慢且容易长时间卡住，这时可以尝试`npm`进行安装

### 使用
使用插件比较的简单，仅需在book.json中增加以下代码
```
"plugins": [
  "-lunr", "-search", "search-pro"
]
```
需要注意的是理论上仅需要`search-pro`即可，但是这个控件要求关闭其他的控件才能正常使用，所以还需要增加`"-lunr", "-search"`这里的`-`则表示关闭某些插件。

---
### search-pro
简介：一个增强的搜索插件，重点是支持中文。  
插件地址：[search-pro](https://plugins.gitbook.com/plugin/search-pro)
### github
简介：在界面的右上角增加一个 GitHub 的小图标，点击该图标则跳转到对应的界面。  
插件地址：[github](https://plugins.gitbook.com/plugin/github)
### splitter
简介：使得侧边栏的宽度可以自由调节。  
插件地址：[splitter](https://plugins.gitbook.com/plugin/splitter)
### toggle-chapters
简介：侧边栏章节可以进行折叠
插件地址：[toggle-chapters](https://plugins.gitbook.com/plugin/toggle-chapters)
### expandable-chapters-small
简介：侧边栏章节可以进行折叠，且显示小箭头
插件地址：[expandable-chapters-small](https://plugins.gitbook.com/plugin/expandable-chapters-small)
