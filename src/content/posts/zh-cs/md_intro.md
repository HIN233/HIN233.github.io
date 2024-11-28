---
title: Learn Markdown the Hard Way
date: 2024-11-27
summary: 对Markdown最基础的介绍，快速上手MD
category: 电子扫盲课
tags: [教程笔记, Markdown]
---

## Title

使用不同数量的#来创建不同层级的标题  
一个#表示一级标题（最大的）  
两个##表示二级（次大）  
以此类推

此外，在文本下方加入任意数量的=表示一级标题,任意数量的-表示二级标题

## Paragraph

使用空白行创建新段落（类比Latex）

## Line Break

使用句末双空格（`结尾空格`）或者`<br>`来换行

## Bold & Italic & Highlight

使用`**两组双星号**`包裹要**加粗**的文字  
此外，若是加粗一个完整的单词，也可以使用 **两组双下划线** （但是如果是单词中间的字母最好不要这么做）

使用`*星号*`包裹要用*斜体*显示的文字  
此外，若是让一个完整的单词变成斜体，也可以使用 _下划线_ （但是如果是单词中间的字母最好不要这么做）

使用 `***两组三星号***` 包裹要用 **_斜体和粗体_** 同时显示的文字  
此外，若是让一个完整的单词变成斜体和粗体同时显示，也可以使用 **_下划线和星号交替使用_** （但是如果是单词中间的字母最好不要这么做）

使用 `==两组双等号==` 包裹要 ==高亮== 的文字

特别地，在VSC里蓝色表示粗体，斜体表示斜体，使用src里面的简单预览较为方便

## Quote

在行首添加`>`可以添加引用  
引用多个段落时在空白行加入`>`可以连接  
使用进行引用嵌套  
可以和其他语法搭配使用

## List

使用数字（开头应从1开始）加英文dot加一个空格来开启一个有序列表，如

1. element1
2. element3
3. element2

使用破折号，星号或加号加一个空格开启一个无序列表，如

- a
- b
- c

使用 一个缩进加其他语法 来嵌套元素

## Code

使用 `` ` `` 包裹代码

若想创建代码块，在代码开头使用一个空白行并每一行Code前加入一个缩进，例如

    Your code

在块首和块莫分别使用三个波浪号` ``` `创建代码块则无需缩进

```c
#include<stdio.h>
int main (void){
    printf("Hello world!\n");
    return 0;
    }
```

## Horizontal Rule

使用`一个空白行+至少三个星号/破折号/下划线+一个空白行`创建一个分割线

---

效果如上

## Link

1. 超链接
2. 网址和Email
3. 和其他语法结合

### 超链接

超链接语法为 `[超链接显示名](超链接地址 "超链接title")`

Code如下  
`[Markdown超链接教程](https://markdown.com.cn/basic-syntax/links.html "官方教程")`

显示效果如下  
[Markdown超链接教程](https://markdown.com.cn/basic-syntax/links.html '官方教程')

Note: title指的是鼠标悬停在超链接上显示的文字

### 网址和Email地址

使用尖括号可以把URL或者email地址变成可点击的链接  
Code如下  
`<1692736302@qq.com>`

显示效果如下  
<1692736302@qq.com>

### 和其他语法结合

基本语法是 `[Name](Address)`  
一个是`**[Name1](Address)**` `*[Name2](Address)*` `*__[Name3](Address)__*`可以加粗显示和斜体显示，效果是 **[Name1](Address)** _[Name2](Address)_ _**[Name3](Address)**_

另一个是

    [`Name`](Address)

可以把**Name**变成Code的外观 [`Name`](Address)

## Picture

插入图片的语法为`![图片alt](图片链接 "图片title")`

添加连接的图片的语法为`[![图片alt](图片链接 "图片title")](地址)`  
本质是Link语法和Picture语法的叠加

## Table

| 元素                                |                语法                 |
| ----------------------------------- | :---------------------------------: |
| Title                               |                  #                  |
| Paragraph                           |             Blank line              |
| Line Break                          |    Trailing whitespace / `<br>`     |
| **Bold** & _Italic_ & ==Highlight== |            `**` `*` `==`            |
| Quote                               |                 `>`                 |
| List                                |      `1. ` / `- `/ `* `/ `+ `       |
| Hortizontal Rule                    |        `---` / `***` / `___`        |
| Link                                |      `[Name](Address "Title")`      |
| Picture                             |      `![alt](Address "Title")`      |
| Table                               |                `\|`                 |
| Task List                           |          `- [ ]` / `- [x]`          |
| Emoji                               | **Copy** Emoji / _Emoji shortcodes_ |

## Task List

在支持任务列表的Markdown应用程序中，使用`- [ ]` / `- [x]`创建任务列表，如下

- [ ] 1
- [x] 1

## Emoji😄

输入emoji可以 _直接复制_ 或输入*emoji shortcodes*  
可以从[Emojipedia](https://emojipedia.org/)等地方直接复制或参考不同程序的Manual获得emoji shortcodes
