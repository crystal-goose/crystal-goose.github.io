---
layout: post
title: 使用githubPages搭建技术博客
---

# 使用github pages搭建技术博客

参考了以下帖子：
https://carl.ac/blogging-with-emacs-org-github-pages/

使用beautifulljekyll的模板搭建博客。帖子统一放置在_posts目录下. 
并不一定要使用org mode。直接在_posts目录下写markdown也挺好的。

使用Org mode，在插入图片、表格、链接、代码等方面还是有明显优势的。但是需要使用Org mode导出成HTML，不能直接使用markdown了。



***

## 附：Markdown语法

斜体： _斜体_

黑体: **黑体**

Headers: 有几个#，就是几级标题

Header不能加粗（bold）,但是可以部分斜体

## Link

### Inline link: [Visit Github](www.github.com)

在Header内也可以使用link

### Reference Link
把inline link后面的括号改成方括号，内置链接的名称，并在其它地方定义该引用。好处是如果有多个相同的链接，更新一次就可以了。相当于先定义链接，然后在其它的地方在引用这个链接。

###　图片
与链接的语法相同，唯一的差异就是前面加感叹号。
#### inline image link

#### reference image link


## code
### inline code
Inline `code` has `back-ticks around` it.

### blocks of code
```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```



## blockquotes（成段引用）
> 准备写Spark MLLib的源代码解析

## Lists

### 无序
### 有序

### 嵌套list
多缩进一个空格

### List with aditional text
文本在list item下空一行，并缩进至少一个空格

## 段落
在markdown源文件中，如果不空行，则不会换行。如果空行，则会增加空行（分段/hard break）。  
在行尾增加两个空格，可以实现soft break。

## 其它
表格。。。
水平分割线：三个hyphens, asterisks, underscors

---




