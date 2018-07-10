---
title: Typora-学习笔记
date: 2018-01-30 20:44:40
categories: 学习
tags: 
- Typora
- Markdown
---

## 字体

*斜体* `* *`
**加粗** `** **` 或者` __ __`
<u>下划线</u> `<u> </u>`
~~删除线~~ `~~ ~~`
代码块
```python
print('hello world!')
```
``` java
System.out.println("Hello World!");
```

 ```markdown
​```语言

balabala

 ```

<!-- more -->


## 有序列表

1. 一一 
2. 二二 
3. 三三 

```markdown
1. 11
2. 22
3. 33
```

## 无序列表

- 周
- 冬 
- 雨

```markdown
- 小
- 黄
- 鸭
-,+,*皆可
```

## 链接

[这个是链接啊](https://www.google.com)

<www.baidu.com>

```markdown
[word](link)
<link>
```

## 引用

> 第一级引用
>
> > 第二级
> >
> > >第三级

```markdown
> 1
	> 2
		> 3
```

## 居中

<center>居中了吗？</center>

```markdown
<center>居中了啦~</center>
```

## 标注（Hexo不支持T_T）

Example[^1]

[^1]: this is a note

```markdown
某些人用过了才知道[^注释]
[^注释]:Somebody that I used to know.
```

## 表格

|  周   |  冬   |  雨   |
| :--: | :--: | :--: |
|  郑   |  茅   |  炜   |
|  在   |  一   |  起   |

 快捷键`Ctrl+T`

## 图片插入

{% asset_img 图片ALT pic.jpg 图片介绍 %}

```markdown
![ALT](image.jpg 图片介绍)
{% asset_img 图片ALT pic.jpg 图片介绍 %}
```

## 多选框（任务列表）

-[ ] 文字—–代表没有选中的复选框


-[x] 文字——代表选中的复选框


-[x] 数学


-[ ] 英语

```markdown
-[空格]空格 文字—–代表没有选中的复选框

-[x]空格 文字——代表选中的复选框

-[x] 数学

-[ ] 英语
```

## 常用快捷键

加粗：`Ctrl+B`

斜体：`Ctrl+I`

字体：`Ctrl+数字`

下划线：`Ctrl+U`

返回开头：`Ctrl+Home`

返回结尾：`Ctrl+End`

生成表格：`Ctrl+T`

创建链接：`Ctrl+K`

---

## References

[Typora学习笔记 - CSDN博客](http://blog.csdn.net/zhangruishi/article/details/70768923#%E9%93%BE%E6%8E%A5%E8%A1%A8%E7%A4%BA)

[Markdown的常用语法(个人总结) - 简书](https://www.jianshu.com/p/82e730892d42)

[Hexo博客搭建之在文章中插入图片](https://yanyinhong.github.io/2017/05/02/How-to-insert-image-in-hexo-post/)

