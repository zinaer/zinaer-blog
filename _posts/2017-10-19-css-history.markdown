---
layout: post
title:  "忆苦思甜，那些斗战 CSS 的岁月"
date:   2017-10-19 11:42:10 +0800
categories: CSS
---
当你想到 HTML 和 CSS 时，你可能会将它们视为一个组合。但是在 Tim Berners-Lee 1989 年首创万维网后多年，并没有类似 CSS 这样的东西。最早的 Web 服务都没有具体的样式设计。

在 WWW 历史邮件列表里有一个这样的[帖子](http://1997.webhistory.org/www.lists/www-talk.1994q1/0648.html)，Marc Andreessen 在 1994 年写道，他将继续创建 Mosaic 和 Netscape 浏览器。Andreessen 在帖子中指出，由于没有办法用 HTML 样式化网站，所以当他被问到视觉效果怎么样时，他唯一可以告诉 Web 开发人员的话是：“糟透了”。

10 年后，CSS 被一个新兴的网络社区全面采用。这期间发生了什么？

#### 发明一种样式语言

关于 Web 的样式，理论上有大量的想法。不过，这不是 Berners-Lee（万维网的发明者）的优先工作，因为他在欧洲核子研究中心的雇主对网络数据目录最感兴趣。相反，我们从社区开发人员那里获得了[几种互相竞争的网页样式语言](https://eager.io/blog/the-languages-which-almost-were-css/)，其中最著名的来自 Pei-Yaun Wei，Andreesen 和 Hakon Wium Lie。

Pei-Yaun Wei 在 1991 年创建了 ViolaWWW 浏览器。他将自己的样式语言添加到这款浏览器中，目标是将该语言变成官方网站标准。虽然最终没能实现这个目标，但确实为其它潜在可能性带来了灵感。

![](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_594,f_auto,q_auto/v1507309739/screengrab_css-violaWWW_sk3dwf.png)

在此期间，Andreessen 在自己的浏览器 Netscape Navigator 中采用了不同的方法。不同于创建专门针对网站样式的解耦语言，他只是将 HTML 扩展为包含可用于设计网页的非标准的 HTML 标签。不幸的是，Web 没多久丢弃了所有语义值，看起来就像这样：

```
<MULTICOL COLS="3" GUTTER="25">
  <P><FONT SIZE="4" COLOR="RED">将被一些字体分解成列</FONT></P>
</MULTICOL>
```

程序员很快意识到这种做法不会持久。有很多替代品，像支持缩写并且简洁的样式语言 RRP，或者 PSL96 支持函数和条件语句的语言。如果你对这些语言感兴趣，Zach Bloom 写过一篇深入了解的[文章](https://eager.io/blog/the-languages-which-almost-were-css/)。

但是，Hakon Wium Lie 在 1994 年 10 月首次提出了引人瞩目的方案，被称为层叠样式表，即 CSS。

#### 为什么要使用 CSS

CSS 的突出是因为它很简单，特别是与其早期的竞争对手相比。

```
window.margin.left = 2cm
font.family = times
h1.font.size = 24pt 30%
```

CSS 是一种声明式编程语言，当我们编写 CSS 时，我们不告诉浏览器必须怎样去渲染页面，相反，我们一步一步描述 HTML 文档的规则，让浏览器决定如何渲染。要知道的是 Web 大部分是由业余程序员和爱好者创建的。CSS 遵循可预测的，更重要的是宽松的格式，使任何人都可以使用它。这是一个特性，而不是 BUG。

CSS 的样式是独一无二的，它允许层叠样式，就像它的名字的表述。这意味着，样式可以继承和覆盖其它已经声明的样式。更为突出的是，它可以在同一个页面显示多种样式。

看到上边例子的百分比值了吗？这是很重要的一点。Lie 认为用户和开发者会渲染出不同的样式，利用这一点浏览器将尽可能友好的渲染页面。百分比，表示样式对某个属性的权重，权重越少，被覆盖的可能性越大。Lie 在第一次演示 CSS 的时候，展示了一个可以在用户和开发者样式之间切换的功能。

在 CSS 早期，这确实是个大的争论，一些人认为，开发者应该有完全的控制权，另一部分人认为，用户应该有控制权。最后，百分比被移除，有利于更明确的规则，明确哪些 CSS 可以覆盖其它样式。无论如何，这是为什么会有差异性。

Lie 发布了他最早的方案后不久，找到了合伙人 Bert Bos。Bos 发明了 Argo 浏览器，拥有自己的样式。后来其中的部分功能加入了 CSS。两个人开始制定更详细的规范，最后向新的 HTML 组织 W3C 的寻求帮助。

花费了几年时间，在 1996 年底，上边的例子变为：

```
html {
  margin-left: 2cm;
  font-family: "Times", serif;
}

h1 {
  font-size: 24px;
}
```

现代样式 CSS 出场了。

#### 浏览器的问题

在 CSS 还是草案期间，网景有支持部分 HTML 标签，像 `multicol`、`layer` 和恐怖的 `blink`。IE 也已经支持部分 CSS，但是它们的支持是有问题的，不彻底的。也就是说，CSS 在作为官方推荐的五年，一直没有浏览器全面支持 CSS。

这是很奇怪的一件事情。

当 Tantek Celik 1997 年加入 Macintosh IE，他的团队很小。一年以后，他的团队被砍到了一半人。明显的原因是，大部分的焦点在 Windows IE，Macintosh IE 更多的是用在自己的设备上。2000 年开发到版本 5，Celik 和他的团队决定把重点放到对 CSS 的支持。

![](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_704,f_auto,q_auto/v1507309819/screengrab_css-MacOS81_svlwca.png)

团队花费两年时间开发版本 5，在此期间，Celik 经常和 W3C 的成员和使用他们浏览器的开发者讨论。对于每一个细节，团队进行验证直到完全正确。最终，在 2002 年三月，他们发布了 Macintosh 版 IE 5，这是第一款全面支持 CSS1 的浏览器。

#### DOCTYPE 声明

要知道的是，Windows 版 IE 已经加入支持 CSS，也带来了一些 BUG 和灵活的盒子模型，描述了元素的计算和渲染。IE 是总宽度和高度内包括边框和填充等属性，但 IE5 for Mac，官方的 CSS 规范要求将这些值添加到宽度和高度。如果你曾经玩过 `box-sizing`，应该知道这个差异。

Celik 知道为了使 CSS 工作，这些差异需要解决。他的解决方案是与标准倡导者 Todd Fahrner 进行讨论，被称为 DOCTYPE 声明。

我们都知道 DOCTYPE，常用于 HTML 的开头。

```
<!DOCTYPE html>
```

但在过去，它们是这样的：

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0//EN" "http://www.w3.org/TR/REC-html40/strict.dtd">
```

这是一个标准的 DOCTYPE 声明例子，重点是 `//W3C//DTD HTML 4.0//EN`。当网页设计师将其添加到他们的页面时，浏览器将页面呈现在“标准模式”中，CSS 将与规范匹配。如果 DOCTYPE 丢失或者已经过时，浏览器会切换到“怪异模式”，并根据旧的盒子模型和旧的 bug 完好无损地进行渲染。有些设计师甚至故意选择把他们的网站置于怪异模式，以获得更旧的（和不正确的）盒子模型。

![](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_500,f_auto,q_auto/v1507309852/screengrab_css-quirksmode_didkmb.jpg)

Eric Meyer 认为，这种切换模式是有必要的，因为我们仍然会使用旧的支持 CSS 的浏览器。

#### 盒子模型 Hack

有一件事要弄清楚，DOCTYPE 声明对于旧的网站在新的浏览器是有效的，但是在旧的浏览器（尤其是 IE）中新网站的盒子模型是不可控的，使用 Celik 聪明的 Hack 技巧，它利用一些 CSS 属性 `voice-family` 来触发浏览器，支持同一个类中的多个宽度和高度，将旧的盒子模型宽度放在前面，用 `voice-family` 关闭标签，然后再放新的模型宽度，比如：

```
div.content {
  width: 400px;
  voice-family: ""}"";
  voice-family: inherit;
  width: 300px;
}
```

`Voice-family` 不被旧的浏览器识别，它被作为字符串看待。所以添加 `}` 在旧的浏览器可以关闭 CSS 规则，在识别第二个宽度之前。这是简单有效的，许多网页开发者开始使用它。

#### 标准的开创者

IE6 发布于 2001 年，最终成为了主流，出现了一些令人深刻的 CSS 标准支持，市场份额更是占据到 80% 左右。

一切准备就绪，人们只要使用 CSS 就可以了。

在过去 10 年，网络无处不在，如果没有一致的或者标准的样式语言，对于网页开发者来说，不会这么简单。相反只能依靠积累的浏览器 hack 技巧，基本的表格布局和嵌入 Flash 来添加一些样式。符合标准，基于 CSS 的设计是新的领域，网络需要这些开创者。

有两个重要的网站，仅隔了几个月，第一个是 **Wired** 紧接着是 **ESPN**。

Douglas Bowman 负责 **Wired** 的 Web 开发团队。在 2002，Bowman 和他的团队发现，没有大型的网站使用 CSS。Bowman 觉得有必要让 **Wired** 成为使用标准 HTML 和 CSS 的范例，所以从头开发该网站。在 9 月份，它被重新开发出来。

![](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_782,f_auto,q_auto/v1507309887/css-wired_xik7fr.gif)

ESPN 在之后的几个月，发布了他们的网站，更广泛的使用了许多相同的技术。这些网站大胆的使用了 CSS 的不少特性，有些技术后来已经被淘汰。但是他们获得了大的成功。如果你找到任何一个参与上述项目的开发者，都可以给到你一份技巧清单。更重要的是，快速的设计改变，易于分享，这些让 Web 变得更好。Wired 甚至做到了每天改变网站的色彩。

![](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_701,f_auto,q_auto/v1507309908/screengrab_css-espn_h3duda.jpg)

查看这些重新设计的网站，你可以找到一些技巧。网页总是显示在固定的几种显示器上，可以注意到两个站点，都使用固定宽度列、相对和绝对定位相结合来实现网页布局，图像用来代替文本，这些网站为 CSS 下一步的发展打下了基础。

#### CSS 禅意花园和语义网

下一年，2003 年，Jeffrey Zeldman 发布了他的书《网站重构》，这本书成为开发者转向标准开发的手册，它揭示了 CSS 技术和技巧的精华，启发开发者思考 CSS 可以做什么。一年以后，Dave Shea 提出了 CSS 禅意花园，估计开发者使用基本的 HTML 加上 CSS 来实现各种布局，该网站展示了最新的技巧和技术，同时还有很长的路要走，直到成为令人信服的标准。

缓慢但确定的势头，高级 CSS，添加新特性。浏览器互相竞争促进实现新的标准，开发者使用了新的技术，最后，CSS 成为了标准。就像一直是这样一样。

[*原文链接*](https://css-tricks.com/look-back-history-css/?utm_source=tuicool&utm_medium=referral)

====

*欢迎关注本站公众号：zinaer666 获取实时免费文章推送*
