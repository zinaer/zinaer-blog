---
layout: post
title:  "你准备使用开源许可证？"
date:   2017-10-23 13:12:10 +0800
categories: licenses
---
你有一个项目，准备使用开源许可证？那么一些问题你必须弄清楚。

你的项目现在处于什么阶段了？完成规划阶段了吗？是和团队一起开发吗？项目是否要分多个模块？等等。

DRY（Don't Repeat Yourself）实现一次是面向对象编程中的基本原则，也是程序员的行事准则。旨在软件开发中，不要重复造轮子。虽然开源项目是最不遵守这个原则的，但是这个原则同样适用于开源项目。

想象一下，假如你的项目最终因为开源许可证使用不当带来了风险，是否会很无奈。最近涉及 Hancom 和 Ghostscript 的开发者 Artifex 的案子，还在审理中，但以下信息是明确的：

为了免费使用 Ghostscript，Hancom 将不得不遵守其使用的开源协议，GNU 通用公共许可证（GPL）。GNU GPL 要求在使用 GPL 授权软件基础上开发的软件，如果公开发布，也必须遵守该协议，进行同等的开放。这意味着 Hancom 必须开源他的软件或者向 Artifex 支付许可费用。

### 评估开源许可证

在准备采用开源许可证之前，下面这些问题，你需要想清楚：

* **你开发的软件是为了什么目的？**是为了开发另一个开源项目？还是为了出售赚钱？
* **别人怎么使用你的软件？**是否可以阅读源代码或者不受限制？
* **你允许别人再怎么分配权限？**是否允许别人重新开发你的项目并出售赚取利润，还是被再分配免费使用？
* **如何处理软件的归属问题？**如果使用了其他开源软件。

这些问题想明白了，还想使用开源协议，那么继续往下看。

### 为什么选择使用开源许可证？

一个原因是使用开源许可证是非常方便的。

开源许可证告诉其他开发者怎么使用你的项目，有什么需要注意的。另外，开源许可证使他人可以很容易为你的项目做贡献，这有助于你的项目变得更好。许可证可以对你的作品进行保护，不至于别人窃取了你劳动成果。

#### 阅读每一个许可证

不是所有的许可证都是一样的，可以参考下面这张来自 choosealicense 的表：

![](http://pic.zinaer.com/201710/licenses.png)

### 常用开源许可证介绍

下面是一些常用开源许可证的介绍，包括使用，权限再分配，以及限制。

#### MIT 许可证

使用这个协议，“被授权人有权利使用、复制、修改、合并、出版发行、散布、再授权和／或出售软件及软件的副本，及授予被供应者同等权利。”意味着你可以很大限度的在你的开发中使用相关软件，唯一需要做的是，你需要在你的软件中包含类似的信息：

>[name of your project] includes code from [original creator of included work] and it is licensed under the MIT License.

并且带上完整的许可证文本。

有一点需要注意，MIT 许可的软件可以集成到 GPL 软件中，但是反过来不可以。意味着如果你的项目同时用到了 MIT 软件和 GPL 软件，最终要保留 GPL 的许可信息。

#### APACHE 许可证

该许可证和 MIT 有些类似，你可以在项目中使用该许可证授权的软件，只要保留版权声明和免责声明。

APACHE 许可证对修改非常严格，你需要明确声明原来作品已经被修改，并在许可协议中包含类似内容：

>The Free Software Foundation considers all versions of the Apache License to be incompatible with the previous GPL versions 1 and 2 and, furthermore, considers Apache License versions before v2.0 incompatible with GPLv3. Because of version 2.0’s patent license requirements, the Free Software Foundation recommends it over other non-copyleft licenses, specifically recommending it either for small programs or for developers who wish to use a permissive license for other reasons.

#### GNU 公共许可证 (GPL) 3

相对于 MIT 许可证，这个许可证不是宽松的，但是确实很大的促进了开源社区的发展，是最常用的开源许可证之一。

如果你使用 GPL，在对外发布时，你需要依据 GPL 许可进行修改 (包括相关文档)。

#### BSD 3 许可证

这同样是一个类似于 MIT 的许可证，允许你使用，再授权和修改，但必须包含版权声明和 BSD 许可证。

你的项目适合 BSD 还是 MIT 需要你来选择。MIT 和 BSD 与其它许可证的兼容也不尽相同。使用 MIT 可以包含其它许可证，但是使用 BSD 就不可以来。

### 不遵守许可证

考虑到不遵守许可证，在将来会带来很大的法律风险，所以在项目没有开始前，就应该避免这种情况的发生。自由软件基金会是一个自愿维护这些规则的组织，他们在一定情况下会主动协调违规者作出相应整改。

#### 许可证兼容

MIT 是相当宽松，所以使用该许可证是一个很好的选择。

最后，虽然国内目前这方面的问题不会很严重，但是版权问题是时代趋势，未雨绸缪，是明智的。

====

![](http://pic.zinaer.com/201710/zanshang.jpg)

<small>*微信扫一扫进行赞赏*</small>

![](http://pic.zinaer.com/201710/zinaer_wx.jpg)

<small>*微信扫一扫关注此公众号*</small>
