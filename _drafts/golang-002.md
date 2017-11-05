---
layout: post
title:  "Go 从入门到放弃系列：入门 二"
date:   2017-11-05 06:35:12 +0800
---
![](http://pic.zinaer.com/201711/golang.jpg)

今天继续来聊，Go 语言入门的一些事儿。

### GIF 动画

下面会演示 Go 语言标准库里 image 这个 package 的用法。

```go
package main

import (
	"image/color"
	"os"
	"io"
	"math/rand"
	"image/gif"
	"image"
	"math"
)

var palette = []color.Color{color.White, color.Black}

const blackIndex  = 1

func main() {
	lissajous(os.Stdout)
}

func lissajous(out io.Writer) {
	const (
		cycles  = 5
		res     = 0.001
		size    = 100
		nframes = 64
		delay   = 8
	)

	freq := rand.Float64() * 3.0
	anim := gif.GIF{LoopCount: nframes}
	phase := 0.0

	for i := 0; i < nframes; i++ {
		rect := image.Rect(0, 0, 2*size+1, 2*size+1)
		img := image.NewPaletted(rect, palette)

		for t := 0.0; t < cycles*2*math.Pi; t += res {
			x := math.Sin(t)
			y := math.Sin(t*freq + phase)
			img.SetColorIndex(size+int(x*size+0.5), size+int(y*size+0.5), blackIndex)
		}
		phase += 0.1
		anim.Delay = append(anim.Delay, delay)
		anim.Image = append(anim.Image, img)
	}
	gif.EncodeAll(out, &anim)
}
``` 

要看这个程序的效果，我们需要将标准输出重定向到一个 gif 图片文件。

```bash
$ go build lissajous.go
$ ./lissajous > out.gif
```

![](http://pic.zinaer.com/201711/out.gif)

当我们 import 一个包含多个单词的 package 时，在使用时用最后一个单词表示这个包就可以了。比如：`image/color` 后面的使用 `color.Color`。

`const` 用来声明常量，常量是指在程序在编译后运行时始终不变的值。

====

![](http://pic.zinaer.com/201710/zanshang.jpg)

<small>*微信扫一扫进行赞赏*</small>

![](http://pic.zinaer.com/201710/zinaer_wx.jpg)

<small>*微信扫一扫关注此公众号*</small>




