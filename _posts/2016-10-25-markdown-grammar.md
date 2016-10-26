---
layout:     post
title:      "Markdown grammar"
subtitle:   "Markdown, Simple，Gammer"
date:       2016-10-25
author:     "Binna"
catalog: true
tags:
    - Markdown
---

### 文字输入
一般正文内容是直接输入  
但是如果想要改变文字字体和改变文字颜色，甚至是文字底色就比较麻烦一点
<br/>
<div align="center"><font face="黑体">我是黑体字</font></div>
<div align="center"><font face="微软雅黑">我是微软雅黑</font></div>
<div align="center"><span style="background:yellow">设置文字底色</span></div>
<center><font color=#0099ff size=5 face="黑体">字体颜色，字体大小，黑体</font></center>
*代码解释*  
居中文字就在文字外面添加一个`<div align="center">text</div>`  

修改文字字体 `<font face="黑体">text</font>`    `<font face="微软雅黑">text</font>`   

修改文字颜色 `<font color=#0099ff >text</font>`    `<font color=red>text</font>`  
支持两种方法，第一种是16进制的代码，第二种是直接写出颜色名字，如red，gray等 

修改文字底色 `<span style="background:#ccc">底色</span>`    `==你好==`  
稍微搜索了以下，发现都是在外面添加表格，但是这样就是一整行了，所以这里使用html的方法创建一个span，在里面添加颜色，这是第一种方法，第二种方法是Markdown语法，就是文字外面加==  

修改文字大小 `<font size=5>text</font>`  
文字size从1到7。3是默认大小。


### 一级标题
一级标题就是在文字前面叫上一个#，#和文字之间不用空格如 `# 一级标题`   



### 二级标题
二级标题就是在文字前面加上二个#，#和空格之间不用空格如 `##二级标题`   



### 三级标题
三级标题就是在文字前面加上三个#，#和空格之间不用空格如 `###三级标题`   



**注意：**最多可以是6级标题，就是最多可以输入6个#   
### 换行
你可能发现自己输入一行之后，回车 <kbd>enter</kbd> 再输入，文字还是显示在一行。这里有两种方法来实现换行，

1. 在文字末尾输入一个`<br/>`
2. 在文字末尾输入两个空格，按两下 <kbd>sapce</kbd>  

### 输入代码
代码的输入是用 <kbd>`</kbd> 来包裹代码，这个键盘符号在键盘左上角，在 <kbd>1</kbd> 左边，在 <kbd>tab</kbd> 上面。在中文输入法下面，按这个键是一个点，在英文输入法下面按这个键会出现我们需要的。

### 键盘按键
用`<kbd></kbd>`包裹文字，就会出现一个不一样的样式。代表是键盘输入的内容。

### 分割线
分割线就是在另起一行输入三个*如 `***`

### 加粗和斜体
在需要加粗的文字外面包裹**，如 `**加粗**`  
在需要斜体的文字外面包裹\*，如 `*斜体*`

### 文字删除线
用<kbd>~~</kbd>包裹文字  
样式如左~~text~~，输入`~~text~~`
<br/>

### 无序列表
* 早饭
* 中饭
* 晚饭

无序刘表就是在文字前面加上一个*和空格如 `* 早饭`
### 有序列表
1. 吃了
2. 没吃
3. 要吃吗

有序列表就是在文字前面加上一序号.和空格如 `1. 吃了`  
<br/>
**注意：**有序列表和无序列表前面有文字的时候,按两下 <kbd>enter</kbd> 开始输入  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;列表后面想跟文字，同样换两次行，按两下 <kbd>enter</kbd> ，就可以重新开始输入

### 引用  
>噫吁嚱，危乎高哉  
>蜀道之难，难于上青天  
>蚕丛及鱼凫，开国何茫然

在文字前面加上>,要是想让多个并列的句子换行，就要在每一个引用句子后面加上两个空格如  
`>噫吁嚱，危乎高哉(加两个空格)`
### 插入链接
格式如左`[链接失效时显示文字](链接 "hover提示字体")`  
样式如左[慕鱼科技](http://www.muyutech.com "慕鱼")
### 插入图片
插入图片有两种样式，但是都需要图床(就是把图片存在别的地方，我们可以用一个链接来拿到图片)，国内很多公司都有自己的服务器，可以做图床，你要是没有自己服务器来放图片，可以使用别人的，这里推荐[七牛](http://www.qiniu.com/)，把图片存放在七牛，然后拷贝链接后之后就可以用了。

1. 插入图片格式如左`![图片失效显示的文字](拷贝的链接 "hover提示文字")`
    ![git ico](http://of6fmev29.bkt.clouddn.com/git.ico)
2. 插入图片格式如下  
   `<img src="拷贝的链接" title="hover提示文字" alt="图片失效显示文字" width="50px" height="50px"/>`  
   使用这种格式来插入的图片可以自己调整图片大小，width代表图片宽度，height代表图片的高度,只输入其中一个参数，另外一个就是自适应的。
   如果我们想要图片居中按下面的格式来  
   `<div align="center"><img src="拷贝的链接" title="hover提示文字" alt="图片失效显示文字" width="50px" height="50px"/></div>`
   <div align="center"><img src="http://of6fmev29.bkt.clouddn.com/git.ico" title="git ico" alt="git ico lost" width="50px"/></div>