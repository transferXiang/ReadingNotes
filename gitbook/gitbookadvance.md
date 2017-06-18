# GitBook 高级功能
## 目录结构
```
.
├── book.json
├── README.md
├── SUMMARY.md
├── styles/
|   ├── website.css
|   └── pdf.css
├── chapter-1/
|   ├── README.md
|   └── something.md
└── chapter-2/
    ├── README.md
    └── something.md
```
以上是官网上推荐的目录结构，下面将简单介绍下各个目录以及文件的作用。
* 目录  
SUMMARY.md
* 简介  
README.md
* 配置文件  
book.json
* 渲染格式  
styles/
* 章节  
chapter-1/  
chapter-2/

## book.json
* 下面的表格是一些基本的字段

| 变量 | 描述 |
| :--- | :---|
| title  | 书名 |
| author | 作者|
| language | 语言 |
| gitbook | 可以指定 gitbook 的版本 |
| plugins | 需要加载的控件 |
| pluginsConfig | 控件的配置参数 |

* 还有一些高级的配置  
**添加链接**
```
"links" : {
"sidebar" : {"Home" : "https://github.com/transferXiang"}
}
```
**自定义渲染风格**
```
"styles" : {
    "website": "styles/website.css",
    "ebook": "styles/ebook.css",
    "pdf": "styles/pdf.css",
    "mobi": "styles/mobi.css",
    "epub": "styles/epub.css"
}
```
**加载控件**
```
"plugins": [
        "-lunr",
        "-search",
        "-highlight",
        "-livereload",
        "github-buttons@2.1.0"
    ]
```
>github-buttons@2.1.0 中的@2.1.0表示指定了该控件的版本   

 **指定控件的配置**
```
"pluginsConfig": {
        "github-buttons": {
            "repo": "zhangjikai/gitbook-use",
            "types": [
                "star"
            ],
            "size": "small"
        }
    }
```
## 生成电子书
* 生成pdf
```
gitbook pdf ./ ./mybook.pdf
```
* 生成ePub
```
gitbook epub ./ ./mybook.epub
```
* 生成Mobi
```
gitbook mobi ./ ./mybook.mobi
```
## 生成封面
只需要在根目录下生成`cover.jpg`即可。为了能够更好的显示，可以在提供一张缩略图`cover_small.jpg`。
推荐的图片尺寸为：`cover.jpg : 1800x2360`、`cover_small.jpg : 200x262`
