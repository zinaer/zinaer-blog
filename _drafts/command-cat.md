---
layout: post
title:  "让文件飞？使用命令行高效地进行文本编辑"
date:   2017-10-27 06:35:12 +0800
---
在这个蔚蓝的星球上，流传着三种文本编辑器：一种是神的编辑器 **Emacs**，一种是编辑器之神 **Vim**，一种是其它。今天我们不想争论谁是最强的编辑器，只是想介绍一些常用的文本处理命令行。我相信，在某些情况下，它们会更快速，更高效。

### cat

使用 cat 来连接文件和标准输入流。

**合并文件**

在终端中，一个或多个文件给到 cat，可以被一起输出和保存。

```bash
$ ls
marks_2015.txt  marks_2016.txt  marks_2017.txt

$ # 同时查看多个文件内容
$ cat marks_201*

$ # 将多个文件的输出内容保存到一个文件
$ cat marks_201* > all_marks.txt
```

**添加内容**

```bash
$ # 在开始添加内容（由 - 的位置来决定）
$ printf 'Name\tMaths\tScience \nbaz\t56\t63\nbak\t71\t65\n' | cat - marks_2015.txt

$ # 在结尾添加内容
$ printf 'Name\tMaths\tScience \nbaz\t56\t63\nbak\t71\t65\n' | cat marks_2015.txt -
```

**删除多余的空行**

```bash
$ #当有多个空行相连，删除多余的，只保留一个空行
$ printf 'hello\n\n\nworld\n\nhave a nice day\n' | cat -s
```

**显示行号**

```bash
$ # 显示所有内容，并包含行号
$ cat -n marks_201*

$ # 显示所有内容，并包含行号，其中空行不计入行号
$ printf 'hello\n\n\nworld\n\nhave a nice day\n' | cat -sb
```

更多显示行号功能，可以参考命令：`nl`

**显示特殊字符**

通过 `$` 界定行尾

```bash
$ 可以看到首行的行位多了空格
$ cat -E marks_2015.txt
Name    Maths   Science $
foo     67      78$
bar     87      85$
```



### 