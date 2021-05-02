---
title: Markdown基本语法
date: 2021-05-02
tags: 语法

---

 

# Markdown

## 基本语法

### 强调

#### 1.粗体/斜体<br>
使用语法：

> \*\*粗体\*\* &emsp; \*斜体\* &emsp; \*\*\*粗体+斜体\*\*\*

 **粗体** &emsp; *斜体* &emsp; ***粗体+斜体***

 #### 2.删除线<br>

使用语法：

> \~\~这句话不要了\~\~

~~这句话不要了~~


#### 3.高亮

当我们需要在一段话中高亮某些关键词，可以用\<html>中的\<span>标签来强调。
> VPN对数据包的处理是 \<span style="background-color:#ffd351"\>通过封装包头(header)\</span\>，继而在GFW外的主机上进行剥离，反之亦然。 

VPN对数据包的处理是 <span style="background-color:#ffd351">通过封装包头(header)</span> ，继而在GFW外的主机上进行剥离，反之亦然。

---

### 引用内容

> 当我们需要引用内容时，可以再前面加 '>'<br>
> 如果需要换行，可以在末尾+两个空格/'\<br\>'
>
> > 这是嵌套引用<br>
> >
> > > 如果吃饱了没事干，可以一直套娃<br>

尽量不要嵌套引用，不美观。

---

### 列表

- 可以用 '*' '+' '-' 作为标记

* 我还是习惯用'-'吧，'\*' 容易与**粗体**搞混

#### 1.有序列表

1. 开头必须是数字，后面必须跟'.'
2. 注意：'.'后面一定要有**空格**
3. 如果下面也有序号列表，当中要空一行，否则序号承接

#### 2.嵌套列表

1. first floor

2. second floor
	1. 2-1
	2. 2-2
3. third floor
	- 有序无序可随意嵌套；
	- 标记后面一定要有空格；
	- 当然，利用转义字符'\.'，它就不再是个列表了；
4. fourth floor
.....

---

### 分割线

分割线必须是3个以上的字符 \*, \-, \_表示, 字符间可以有空格，但不能有其他字符

> \*\*\* &emsp; \- \- \- &emsp; \_ \_\_

显示：(分割线)

---

### 表格
使用语法：
"|" 分隔单元格，"-" 分隔表头和行
> \| name \| age |
> \| :----:    \| :--- |
> \| Twyz  \| 24 |
> \| Jenny \| 25 |

| name | age |
| :----: | :--- |
| Twyz | 24 |
| Jenny | 25 |

表头下方的分割线标记，代表了对齐方式：

- **:---** 左对齐
- **:---:** 居中对齐
- **---:** 右对齐

> \| left \| center \| right \| 
> \|:---- \| :----: \| ----: \|
> \| aaaa \| bbbbbb \| ccccc \| 
> \| a  \|  b  \|  c  \|

| left | center | right |
| :--- | :----: | ----: |
| aaaa | bbbbbb | ccccc |
|  a |  b  |  c  |

---

### 超链接

使用语法：

> \[markdown基本语法](https://xianbai.me/learn-md/index.html)\<br>

[markdown基本语法](https://xianbai.me/learn-md/index.html)<br>
或者直接用原地址：<http://www.baidu.com/><br>
这适合较短的网址

---

### 图片

使用语法：

> \![panda]\(https://avatars2.githubusercontent.com/u/3265208?v=3&s=100 "GitHub,Social Coding")

![GitHub](https://avatars2.githubusercontent.com/u/3265208?v=3&s=100 "GitHub,Social Coding")

也可设置图片大小

``` html

<img src="https://avatars2.githubusercontent.com/u/3265208?v=3&s=100" alt="GitHub" title="GitHub,Social Coding" width="50" height="50" />

```
<img src="https://avatars2.githubusercontent.com/u/3265208?v=3&s=100" alt="GitHub" title="GitHub,Social Coding" width="70" height="70" />

---

### 代码块
使用语法：

```  c
int main()
{
	int x = 0;
}
```

---
### 表情符号

使用语法：

> :\<表情代码\>:

举例：
> :smile:  &emsp; &emsp; smile
> :laughing:  &emsp; &emsp; laughing
> :+1:  &emsp; &emsp; +1
> :clap:  &emsp; &emsp; clap

更多的表情，请参考：[webpage-tool](https://www.webfx.com/tools/emoji-cheat-sheet/)<br>



---

