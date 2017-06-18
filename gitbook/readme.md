# GitBook基础
## GitBook简介
GitBook 是一个命令行工具。它基于 Node.js 、 Markdown 、 git 等，可以为你创建美观的书籍，通常它可以导出为网页或电子书（pdf、epub、mobi）。

GitBook 和 GitBook.com 不是同一个概念，一个是工具，一个是网站。他们之间的关系类似于 Git 与 GitHub。通过 GitBook 创建的书籍可以通过 GitBook.com 进行线上存储和管理。同时 GitBook.com 与 GitHub 账号以及仓储是可以进行绑定与同步的，因此 Gitbook.com 中的文字等都可以在 GitHub 上进行托管，这对熟悉 Git 以及 GitHub 的用户（特别是程序员）来说是一种全新的方式管理个人文档，更将在编程领域中的一些先进的团队协作工作流引入到书籍创作中来。

## GitBook安装
1. 安装Node.js

 由于 GitBook 基于 Node.js 所以必须先安装它。安装它非常简单，上网下载安装包按照说明一步一步安装即可。
2. 安装GitBook

 NPM 是随同 NodeJS 一起安装的包管理工具，能解决 NodeJS 代码部署上的很多问题，常见的使用场景有以下几种：
 * 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
 * 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
 * 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

 打开命令行工具，输入一下指令回车即可进行安装（安装过程可能比较慢、或者失败，多试几次）
 ```
 npm install gitbook-cli -g
 ```
 如果安装完成后执行 gitbook 语句，如果没有提示错误则说明安装成功。

3. 创建第一本书

 * 创建一个 GitBook 项目
```
gitbook init
```
通过以上操作会生成两个文件
```
.
├── README.md
└── SUMMARY.md
```
其中README.md的内容相当于整个书的简介。而SUMMARY则是书的目录。

 * 生成静态网页
 ```
 gitbook build
 ```
  以上命令会在当前目录下生成一个 \_book 的文件夹，文件夹内有一个index.html的网页，通过浏览器就可以查看该书籍的网页版。

 * 生成带服务器的网页
 ```
 gitbook serve
 ```
  通过以上命令可以生成一个带有服务器的网页，可以通过访问 "http://localhost:4000" 对该网页进行浏览。

## GitBook相关资源
* [GitBook 使用简介](https://github.com/zhangjikai/gitbook-use)
* [官方帮助文档](https://help.gitbook.com/)
* [GitBook Toolchain Documentation](https://toolchain.gitbook.com/)
* [使用gitbook制作属于自己的电子书](https://www.zybuluo.com/yangfch3/note/158290)
