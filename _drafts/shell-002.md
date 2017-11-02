---
layout: post
title:  "玩转 shell 系列之初识 shell 二"
date:   2017-11-02 06:12:10 +0800
---
Linux 是世界上最强大、最灵活的操作系统之一，而 shell 是同 Linux 进行交互的最灵活的方式。

### 终端信息

处理终端信息，是 shell 经常处理的任务。有两款工具，tput 和 stty 可以使用。

```bash
# 获取终端行数
$ tput cols
# 获取终端列数
$ tput lines

# 打印当前终端名
$ tput longname
# 把光标移动到坐标（100,100）处
$ tput cup 100 100
# 设置文本样式为粗体
$ tput bold
```

```bash
#!/usr/bin/env bash
echo -e 'Enter password:'
stty -echo
read password
stty echo
echo                                                  
echo 'Password read.'
```

上述例子，使用 `stty -echo` 令密码输入不可见。

### 获取、设置日期和延时

很多应用程序需要以不同的格式打印日期、设置日期和时间、根据日期和时间或延时执行操作。

```bash
# 读取日期
$ date
Wed Nov  1 14:30:20 CST 2017
# 打印 Unix 时间戳（从 1970年1月1日0时0分0秒以来的秒数）
$ date +%s
1509517903
# 将日期转换成时间戳
$ date --date 'Wed Nov  1 14:30:20 CST 2017' +%s
1509517820
# 将日期转换成星期
$ date --date 'Wed Nov  1 14:30:20 CST 2017' +%A
Wednesday

# 格式化时间戳
$ date '+%B %d %Y'
November 01 2017
# 设置时间
$ date -s 'Wed Nov  1 14:39:08 CST 2017'
```

```bash
#!/usr/bin/env bash
start=$(date +%s)
sudo apt update
end=$(date +%s)
difference=$(( end - start ))
echo "Time taken to execute commands is $difference seconds."
```

上述脚本可以，计算出 `sudo apt update` 命令执行了多长时间。也可以使用 `time sudo apt update` 获取。

```bash
#!/usr/bin/env bash
echo 'Hello'
sleep 5
echo 'world!'
```

上述，通过 sleep 延迟了 5 秒，才会输出后面的 world。

### 调试脚本

调试功能是每一种编程语言都应该实现的重要特性之一，当出现一些始料未及的情况时，用它来生成脚本运行信息，帮助弄清什么原因导致的。

```bash
# -x 可以打印出每一行命令以及状态
$ bash -x script.sh
```

```bash
# 部分调试
#!/usr/bin/env bash
echo 'Hello'
set -x
sleep 5
set +x
echo 'world!'
```

```bash
set -x 在执行时显示参数和命令
set +x 禁止调试
set -v 当命令进行读取时显示输入
set +v 禁止打印输入
```

另外，也可以使用 `#!/usr/bin/env bash -xv` 进行调试。

### 函数和参数

和其它语言一样，bash 同样支持函数。

```bash
# 定义函数、调用和传参
name() {
	echo $1, $2; # 参数 1 和参数 2
	echo "$@"; # 打印所有参数
	echo "$*"; # 同 $@，但是参数被一起作为单个实体，不常用

	return 0;
}
name 'zinaer' 'com'
```

```bash
# 递归函数
name() {
	echo $1;
	name Hello;
	sleep $1;
}
```

上述递归函数，会调用自己，不断生成新的进程，最终造成拒绝服务，被称为 Fork 炸弹。
