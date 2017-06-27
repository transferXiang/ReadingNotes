# MarkDown 显示公式
## Latex公式生成
Latex公式如果不会写的话，可以通过在线的方式生成；地址为：  
[codecogs](http://latex.codecogs.com/eqneditor/editor.php)

## 在线方式显示
### 使用Google Chart的服务器
```
<img src="http://chart.googleapis.com/chart?cht=tx&chl= 在此插入Latex公式" style="border:none;">
```
比如
```
<img src="http://chart.googleapis.com/chart?cht=tx&chl=\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" style="border:none;">
```
显示为公式时为：  
<img src="http://chart.googleapis.com/chart?cht=tx&chl=\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" style="border:none;">


## 插件的方式显示
### KaTex插件
比如 '\$\$ x=\frac{-b\pm\sqrt{b^2-4ac}}{2a} \$\$' 显示为：$$ x=\frac{-b\pm\sqrt{b^2-4ac}}{2a} $$  
**注意，这里显示的不是图片，而是文字**
